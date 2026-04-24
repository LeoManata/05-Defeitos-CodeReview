# 🐛 Bug Reports — Parte A

**Dupla:** [Givanne Feitosa - RA 223671] + [Leonardo Manata - RA 216864]
**Data da exploração:** [23/04/2026]
**Navegador usado:** [Chrome 121]
**Sistema operacional:** [Windows 11]

---

## BUG-001

**Título:** Criação de tarefas idênticas

**Severidade:**  Média
**Justificativa da severidade:** A criação de tarefas idênticas pode resultar na confusão do usuário e do próprio programa, pois pode ler a informação incorretamente e tomar alguma atitude indesejada.


**Prioridade:** P1 
**Justificativa da prioridade:** Por se tratar de um "To Do" tem de ser corrigido rapidamente para que não interfira no resultado das tarefas

**Ambiente:**
- Navegador: [Chrome 121.0]
- Sistema Operacional: [Windows 11]
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1. Acessar a aplicação
2. Criar duas tarefas com  o mesmo título, categoria, prazo, prioridade e confirmar a criação

**Resultado esperado:**
Deveria impedir que a tarefa fosse criada pois já existiria uma com as mesmas informações.

**Resultado obtido:**
A tarefa é criada duplicadamente.

**Evidência:**
Print evidenciando a criação de duas tarefas duplicadas
<img width="713" height="772" alt="image" src="https://github.com/user-attachments/assets/99bc46e8-7cdc-4b3d-86d6-ca305a3009ce" />


---


## BUG-002

**Título:** Criação de tarefa sem prioridade (NaN)

**Severidade:** Alta
**Justificativa da severidade:** A ausência de um valor de prioridade válido no campo, pode acarretar no mal funcionamento da filtragem das tarefas

**Prioridade:** P1
**Justificativa da prioridade:** Um campo obrigatório retornando valor inválido afeta diretamente funcionalidades que dependem da prioridade (ex: ordenação, notificações, filtros).

**Ambiente:**
- Navegador: Chrome 121.0
- Sistema Operacional: Windows 11
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1. Acessar a aplicação
2. Iniciar a criação de uma nova tarefa
3. Deixar o campo "Prioridade" vazio e adicionar tarefa

**Resultado esperado:** 
A aplicação deveria impedir a criação da tarefa e exibir uma mensagem de validação informando que o campo "Prioridade" é obrigatório

**Resultado obtido:**
A tarefa é criada com o valor de prioridade como NaN, indicando que nenhuma validação está sendo aplicada no campo de prioridade

**Evidência:**
<img width="710" height="618" alt="image" src="https://github.com/user-attachments/assets/ecdf05c3-a508-425c-b9a5-6088ad512dc4" />

---

## BUG-003

**Título:** Criação de tarefa sem título

**Severidade:** Alta
**Justificativa da severidade:** O título é o principal identificador de uma tarefa e sem ele a tarefa se torna impossível de identificar e saber do que se trata

**Prioridade:** P1
**Justificativa da prioridade:** Campo obrigatório sem validação compromete a identificação da tarefa e a usabilidade básica do sistema.

**Ambiente:**
- Navegador: Chrome 121.0
- Sistema Operacional: Windows 11
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1. Acessar a aplicação
2. Iniciar a criação de uma nova tarefa
3. Deixar o campo "Título" vazio e confirmar a criação

**Resultado esperado:**
A aplicação deve bloquear a criação da tarefa "fantasma" e exibir uma mensagem indicando que o campo "Título" é obrigatório

**Resultado obtido:**
A tarefa é criada sem título

**Evidência:**
<img width="726" height="702" alt="image" src="https://github.com/user-attachments/assets/ee5d67a0-3bf2-4696-8091-bbecf22e3bfe" />


---


<!-- Para reports adicionais, copie o bloco acima trocando o número. -->

---

## ✅ Critérios de qualidade do bug report
*(Use para conferir antes de entregar)*

- [✅] Título descritivo — outra pessoa entende o problema só pelo título?
- [✅] Passos são **numerados** e **reproduzíveis** por terceiros?
- [✅] Há **pelo menos uma evidência** (screenshot, GIF ou log)?
- [✅] Severidade tem **justificativa explícita**?
- [✅] Prioridade tem **justificativa explícita**?
- [✅] Ambiente inclui **navegador + SO**?
- [✅] "Esperado vs. Obtido" deixa o gap claro?

## ✅ Checklist de qualidade dos reports

Antes de submeter, confirme em cada report:

- [✅] Título é específico e acionável (não `"Não funciona"`).
- [✅] Passos estão **numerados** e são reproduzíveis por terceiros.
- [✅] Há **pelo menos uma evidência** por report (imagem, GIF ou log).
- [✅] Severidade tem **justificativa explícita**.
- [✅] Prioridade tem **justificativa explícita**.
- [✅] Ambiente inclui **navegador + SO**.
- [✅] "Esperado × Obtido" deixa a diferença clara.
- [✅] Os 3 defeitos reportados cobrem **categorias diferentes**
      (funcional, UX, validação, persistência, etc.)
