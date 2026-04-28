# SOC Labs – Raphael Orfali

## Lab 2 – Phishing Email Triage and IOC Analysis

### Cenário
Este laboratório simula o recebimento de um email suspeito reportado por um usuário interno após uma mensagem com aparência de cobrança urgente e solicitação de ação imediata.

O objetivo é realizar a triagem inicial do email, analisar remetente, domínio, links e cabeçalhos, identificar indicadores de comprometimento e classificar o incidente.

---

### Objetivo
Determinar se o email analisado é legítimo ou malicioso, justificar a conclusão com base em evidências técnicas e documentar as ações recomendadas de contenção.

---

### Principais Achados
- Remetente com domínio suspeito tentando imitar marca conhecida
- Linguagem de urgência e cobrança para induzir clique imediato
- Link direcionando para domínio não relacionado ao suposto emissor
- Inconsistências em `Return-Path`, `Reply-To` e origem da mensagem
- Evidências compatíveis com phishing de coleta de credenciais

---

### Resumo do Incidente
Severidade: Alta

Status: Confirmado

Categoria: Phishing

IOC Principal: `portal-faturas-support.com`

Usuário Impactado: `financeiro@empresa.local`

---

### Fluxo de Investigação
1. Revisão do conteúdo do email e da narrativa usada para pressionar a vítima.
2. Validação do domínio do remetente e do link enviado.
3. Análise dos cabeçalhos para identificar inconsistências na origem.
4. Extração de IOCs relevantes para bloqueio e hunting.
5. Classificação do incidente e definição de ações imediatas.

---

### Ações Recomendadas
- Bloquear o domínio malicioso em proxy, firewall e secure email gateway.
- Bloquear a URL utilizada na campanha.
- Verificar se houve clique ou submissão de credenciais.
- Notificar o usuário impactado e orientar troca de senha em caso de interação.
- Executar busca por emails semelhantes em outras caixas postais.

---

## Evidências

Artefatos analisados:
- [email.txt](email.txt)
- [email-headers.txt](email-headers.txt)
- [incident-report.md](incident-report.md)

---

### Competências Demonstradas
- triagem inicial de email suspeito
- análise de headers
- identificação de IOC
- análise de domínio e URL suspeita
- classificação de phishing com base em evidências
- definição de contenção inicial

---

## Observações
Este laboratório representa um cenário simulado para fins de estudo e prática em triagem de phishing e análise inicial de incidente.
