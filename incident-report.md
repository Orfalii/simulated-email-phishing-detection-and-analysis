# Incident Report – Phishing Email Triage

## Data
15/04/2026

## Objetivo
Analisar um email suspeito reportado por usuário interno, identificar sinais de phishing, extrair indicadores de comprometimento e classificar o incidente com base nas evidências disponíveis.

---

## Resumo Executivo
Foi analisado um email enviado para `financeiro@empresa.local` com falsa aparência de cobrança Microsoft 365 e linguagem de urgência para induzir ação imediata.

O conteúdo, os cabeçalhos e o link embutido apresentam múltiplos sinais de fraude, incluindo domínio typosquatting, falha de SPF, ausência de DKIM, falha de DMARC e divergência entre remetente e `Reply-To`.

Conclusão: trata-se de um email de phishing com provável objetivo de coleta de credenciais.

---

## Escopo da Análise
- Artefato principal: [raw-email.txt](raw-email.txt)
- Cabeçalhos analisados: [email-headers.txt](email-headers.txt)
- Usuário alvo: `financeiro@empresa.local`
- Tema utilizado: cobrança pendente Microsoft 365
- IOC principal: `portal-faturas-support.com`

---

## Detecção
O caso teve início após o usuário reportar um email com tom de urgência, informando possível suspensão de serviço caso uma validação de pagamento não fosse realizada no mesmo dia.

Na triagem inicial, os principais pontos suspeitos foram:
- remetente tentando se passar por Microsoft
- domínio com aparência enganosa
- link não relacionado ao domínio legítimo da marca
- inconsistências de autenticação do email

---

## Linha do Tempo
- 08:14:22 -> email recebido por `financeiro@empresa.local`
- 08:16:00 -> mensagem reportada como suspeita pelo usuário
- 08:22:00 -> análise manual do conteúdo e dos headers iniciada
- 08:31:00 -> IOCs identificados e classificação do caso concluída

---

## Evidências Técnicas
- `From`: `billing@micr0soft-billing-support.com`
- `Reply-To`: `atendimento@portal-faturas-support.com`
- URL enviada: `https://portal-faturas-support.com/secure/m365-validation`
- IP de origem observado: `45.77.188.201`
- `SPF = fail`
- `DKIM = none`
- `DMARC = fail`
- Uso de display name confiável para mascarar remetente suspeito
- Linguagem de pressão: "ação necessária hoje" e "próximas 2 horas"

---

## Análise
O email apresenta sinais clássicos de phishing voltado para roubo de credenciais:

1. O remetente utiliza uma variação visual de marca conhecida, substituindo letras para induzir erro de percepção.
2. O domínio do link não corresponde ao suposto serviço representado no corpo da mensagem.
3. O `Reply-To` difere do remetente principal, indicando possível redirecionamento da interação para infraestrutura controlada por atacante.
4. Os controles básicos de autenticação falharam ou estão ausentes, o que enfraquece qualquer hipótese de legitimidade.
5. O contexto de cobrança urgente aumenta a probabilidade de clique por parte de usuários de áreas financeiras e administrativas.

Com base nesses elementos, a hipótese de mensagem legítima deve ser descartada.

---

## Impacto Potencial
- roubo de credenciais corporativas
- comprometimento de conta de usuário
- acesso inicial a sistemas internos
- reutilização de credenciais em portais SaaS
- expansão da campanha para outras vítimas internas

---

## Indicadores de Comprometimento (IOCs)
- Domínio suspeito: `micr0soft-billing-support.com`
- Domínio do link: `portal-faturas-support.com`
- IP observado: `45.77.188.201`
- Assunto: `[Urgente] Pagamento pendente - ação necessária hoje`
- Conta alvo conhecida: `financeiro@empresa.local`

---

## Classificação do Incidente
- Severidade: Alta
- Status: Confirmado
- Tipo: Phishing

Justificativa:
Há evidências suficientes de fraude por engenharia social combinada com infraestrutura suspeita e falhas de autenticação de email. O material analisado é compatível com campanha de phishing voltada para coleta de credenciais.

---

## Ações Recomendadas
- bloquear `portal-faturas-support.com` e `micr0soft-billing-support.com`
- bloquear o IP `45.77.188.201` nos controles aplicáveis
- pesquisar mensagens semelhantes em outras caixas postais
- verificar se o usuário clicou no link
- resetar senha e revogar sessões caso tenha havido interação
- registrar os IOCs no processo de monitoramento
- reforçar conscientização para equipes financeiras

---

## Conclusão
O email analisado deve ser tratado como phishing confirmado.

A combinação entre engenharia social, domínio enganoso, link suspeito e falhas de autenticação torna o caso forte o suficiente para contenção imediata e hunting interno por mensagens similares.
