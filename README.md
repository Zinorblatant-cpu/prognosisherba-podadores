# prognosisherba-podadores

App das equipes de poda do **PrognosisHerba**. Feito para o celular, em
campo: a equipe escolhe quem é, vê os locais do dia em ordem de
prioridade e marca cada um como concluído.

- Sem login: a equipe escolhida fica salva no próprio aparelho
  (`localStorage`).
- A agenda é a última alocação publicada pelo
  [painel](https://github.com/Zinorblatant-cpu/prognosisherba-painel).
- O que a equipe marca como concluído aparece ao vivo na tela de
  Monitoramento do painel.

Faz parte de um conjunto de repositórios:

| Repositório | Papel |
|---|---|
| [prognosisherba-api](https://github.com/Zinorblatant-cpu/prognosisherba-api) | Previsões, solver e alocação publicada. **Este app precisa dela no ar** |
| [prognosisherba-painel](https://github.com/Zinorblatant-cpu/prognosisherba-painel) | Painel de planejamento do gestor |
| **prognosisherba-podadores** (este) | App das equipes em campo |
| [prognosisherba-docs](https://github.com/Zinorblatant-cpu/prognosisherba-docs) | Documentação completa: arquitetura e modelos matemáticos |

## Rodando

Node.js 20 ou mais novo, com a
[prognosisherba-api](https://github.com/Zinorblatant-cpu/prognosisherba-api)
rodando em `http://127.0.0.1:8002`.

```bash
cp .env.example .env
npm install
npm run dev        # http://localhost:5174
```

| Variável | Padrão | O que faz |
|---|---|---|
| `VITE_API_BASE_URL` | `http://127.0.0.1:8002` | Endereço da API. É embutida no build: se mudar, rode o build de novo |

Rotas da API usadas: `GET /alocacao/atual` e
`POST /alocacao/locais/concluir`.

## Scripts

| Comando | O que faz |
|---|---|
| `npm run dev` | Servidor de desenvolvimento |
| `npm run build` | Checagem de tipos + build de produção em `dist/` |
| `npm test` | Testes (Vitest + Testing Library) |
| `npm run test:coverage` | Testes com cobertura; reprova abaixo de 100% |
| `npm run lint` | Lint com oxlint |

## Stack

React 19 · Vite 8 · TypeScript · Tailwind 4

## Estrutura

```
src/
├── components/   Agenda, SeletorEquipe, PriorityTag, DifficultyTag
└── lib/          api, equipe (localStorage), locais (ordenação), formato
```

## Hospedagem

O build gera arquivos estáticos em `dist/`. A hospedagem precisa
redirecionar todas as rotas para `index.html` (`/* → /index.html`).
