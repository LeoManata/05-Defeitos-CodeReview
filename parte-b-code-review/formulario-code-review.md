# 🔎 Formulário — Parte B

> Preencha uma seção por finding. O mínimo esperado é **6 findings**.

**Dupla:** [Giovanne Feitosa - RA 22367] + [Leonardo Manata + 216864]
**Data da revisão:** [23/04/2026]

---

### Finding #1

**📍 Linha(s): buscarUsuarioPorNome
**🏷 Rótulo: blocker
**📂 Dimensão: Segurança
**⚠️ Severidade: Crítica

**🐛 Problema:**
Concatenação direta de input do usuário na query SQL. Vulnerabilidade clássica de SQL Injection. Um valor como ' OR '1'='1 no campo nome expõe toda a tabela

**💡 Sugestão de correção:**

```javascript
return db.executarQuery('SELECT * FROM usuarios WHERE nome = ?', [nome]);
```

---


### Finding #2

**📍 Linha(s): cadastrarUsuario, atualizarEmail, listarUsuariosAtivos, buscarUsuarioPorNome
**🏷 Rótulo: blocker
**📂 Dimensão: Erros
**⚠️ Severidade: Crítica

**🐛 Problema:
Nenhuma função async possui try/catch. Falhas de banco ou de hash propagam exceções não tratadas, podendo derrubar a aplicação silenciosamente.

**💡 Sugestão de correção:**

```javascript
async function cadastrarUsuario(dados) {
  try {
    const senhaHash = await crypto.hash(dados.senha, 10);
    const usuario = { ...dados, senha: senhaHash, ativo: true, criadoEm: new Date().toISOString() };
    await db.insert('usuarios', usuario);
    logger.info('Usuario cadastrado: ' + dados.email);
    return usuario;
  } catch (err) {
    logger.error('Erro ao cadastrar usuario: ' + err.message);
    throw err;
  }
}
```

---

### Finding #3

**📍 Linha(s): atualizarEmail
**🏷 Rótulo: major
**📂 Dimensão: Erros
**⚠️ Severidade: Alta

**🐛 Problema:
O retorno de db.buscarPorId não é verificado antes do uso. Se o ID não existir, u será null e a linha u.email = novoEmail lançará um TypeError em runtime.

**💡 Sugestão de correção:**

```javascript
async function atualizarEmail(id, novoEmail) {
  const u = await db.buscarPorId('usuarios', id);
  if (!u) throw new Error(`Usuário com id ${id} não encontrado.`);
  u.email = novoEmail;
  await db.atualizar('usuarios', id, u);
  logger.info('Email atualizado para usuario id: ' + id);
  return u;
}
```

---

### Finding #4

**📍 Linha(s): cadastrarUsuario
**🏷 Rótulo: major
**📂 Dimensão: Segurança
**⚠️ Severidade: Alta

🐛 Problema:
Nenhum campo é validado antes da inserção. nome, email, senha e tipo podem chegar vazios ou inválidos. TIPOS_VALIDOS está definido no arquivo mas nunca é utilizado.

**💡 Sugestão de correção:**

```javascript
async function cadastrarUsuario(dados) {
  if (!dados.nome || !dados.email || !dados.senha) {
    throw new Error('Campos obrigatórios ausentes: nome, email e senha.');
  }
  if (!TIPOS_VALIDOS.includes(dados.tipo)) {
    throw new Error(`Tipo de usuário inválido: "${dados.tipo}".`);
  }
  // ...resto da função
}
```

---

### Finding #5

**📍 Linha(s): calcularLimiteEmprestimo, calcularLimiteComSuspensao
**🏷 Rótulo: major
**📂 Dimensão: Complexidade
**⚠️ Severidade: Média

🐛 Problema:
As duas funções implementam a mesma lógica com pequenas variações e sem reaproveitamento — violação do princípio DRY. Qualquer mudança na regra de negócio precisa ser replicada nos dois lugares, aumentando o risco de inconsistência.

**💡 Sugestão de correção:**

```javascript
function calcularLimiteEmprestimo(usuario, { verificarSuspensao = false } = {}) {
  if (verificarSuspensao && usuario.suspenso) return 0;
  if (usuario.bloqueadoAte && new Date(usuario.bloqueadoAte) > new Date()) return 0;

  if (usuario.tipo === 'professor') return _limiteProfessor(usuario);
  if (usuario.tipo === 'aluno') return _limiteAluno(usuario);
  return 5;
}
```

---

### Finding #6

**📍 Linha(s): logger.info('Email atualizado: ' + novoEmail)
**🏷 Rótulo: nit
**📂 Dimensão: Segurança
**⚠️ Severidade: Baixa

**🐛 Problema:
O e-mail do usuário é logado em texto puro. Dependendo do destino dos logs, isso pode expor dados pessoais e violar políticas de privacidade como a LGPD.

**💡 Sugestão de correção:**

```javascript
logger.info(`Email atualizado para usuario id: ${id}`);
```

---

## ✅ Checklist final

- [✅] Há pelo menos 6 findings preenchidas
- [✅] Cada finding cita linha, dimensão, rótulo e severidade
- [✅] As sugestões são concretas e acionáveis
- [✅] Pelo menos uma finding cobre segurança
- [✅] Pelo menos uma finding cobre complexidade
