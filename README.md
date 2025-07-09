# bug-report
# 🐞 BUG REPORT CLONE (n8n Workflow)

Este é um workflow n8n para **captura, registro e notificação automática de bugs**. Ele recebe dados via webhook, processa as informações, salva no banco de dados (Supabase/PostgreSQL) e envia alerta no Discord.

---

## 📌 O que ele faz

1. **Recebe requisições POST** com dados de bug via Webhook
2. **Processa e valida os dados** recebidos com um node de código
3. **Registra o bug** na tabela `notificacoes_bug` do Supabase
4. **Envia notificação** em um canal do Discord (via webhook)

---

## 🔧 Estrutura dos Nodes

| Ordem | Node                      | Função                                                                 |
|-------|---------------------------|------------------------------------------------------------------------|
| 1     | `Webhook`                 | Recebe requisições POST com dados do bug                              |
| 2     | `Code`                    | Extrai e formata os campos: `origin`, `severity`, `message`, etc      |
| 3     | `Execute a SQL query`     | Insere os dados na tabela `notificacoes_bug` (PostgreSQL/Supabase)    |
| 4     | `Discord`                 | Envia aviso em tempo real com `@everyone` sobre o novo bug            |

---

## 📥 Estrutura esperada do JSON (corpo do webhook)

```json
{
  "origin": "frontend",
  "severity": "high",
  "message": "Erro ao carregar a página",
  "context": {
    "userId": 1,
    "page": "/chat",
    "timestamp": "2025-07-08T20:43:00.000Z"
  }
}
