# Sistema de RH — Hub dos Restaurantes

Plataforma completa de recrutamento com triagem automatizada de curriculos por IA.

**Demo em producao:** [hubdosrestaurantes.com.br/vagas](https://hubdosrestaurantes.com.br/vagas/)

---

## Arquitetura

```
Candidato preenche formulario
        |
        v
  [Site de Vagas]  ──────────────>  [API / VPS]
  index.html                              |
                                          v
                                   [n8n Workflow]
                                   RH-ANALISE-CURRICULOS
                                          |
                                          v
                                   [Gemini AI]
                                   Le e resume o curriculo
                                   Classifica o candidato
                                          |
                                          v
                                   [RH recebe analise]
                                   via WhatsApp / painel admin
```

---

## Componentes

### Frontend publico (`index.html`)
- Listagem de vagas com filtros por cargo e localizacao
- Formulario de candidatura com upload de curriculo
- Design responsivo mobile-first

### Painel Admin (`admin.html`)
- Autenticacao com login seguro
- Criacao e edicao de vagas em tempo real
- Visualizacao de candidatos por vaga com curriculo
- Filtros por status, data e cargo

### Automacao n8n — `RH-ANALISE-CURRICULOS`
- Dispara quando novo curriculo e recebido
- Le o PDF do curriculo via OCR
- Envia para Gemini AI com prompt de triagem
- Classifica o candidato por fit com a vaga
- Resume pontos fortes e alertas
- Notifica o RH com a analise completa

---

## Stack

| Camada | Tecnologia |
|---|---|
| Frontend | HTML · CSS · JavaScript |
| Backend | Node.js · REST API · VPS |
| Automacao | n8n |
| IA | Gemini |
| Infra | Linux VPS · Nginx |

---

## Configuracao

Substitua os placeholders no codigo pelos valores do seu ambiente:

| Placeholder | Onde | O que e |
|---|---|---|
| `YOUR_API_URL` | `admin.html` | Endpoint base da API REST |
| `YOUR_N8N_WEBHOOK_URL` | `index.html` | Webhook do workflow n8n |
| `YOUR_SENHA_SALT` | `admin.html` | Salt para hash de senha |

---

## Nota sobre seguranca

Esta e a **versao demo** publicada para portfolio. Credenciais, endpoints e
o salt foram substituidos por placeholders.

Na versao demo a autenticacao do admin e resolvida no client-side para
simplicidade de demonstracao. **Em producao**, a validacao de credenciais,
o controle de acesso e a triagem de curriculos rodam no backend (VPS + n8n),
nunca no navegador — o frontend apenas consome a API ja autenticada.
