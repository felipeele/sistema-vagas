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

Substitua `YOUR_API_URL` no codigo pelo endpoint da sua API.
