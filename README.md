# ReportFlow

ReportFlow é uma aplicação full-stack local para coletar dados operacionais, consolidar indicadores e distribuir relatórios automaticamente. Ela roda sem credenciais externas e sem serviços pagos: os conectores de API, e-mail e Slack são simulados, mas o armazenamento, importação, geração de PDF, histórico, logs e agendamentos são persistidos de verdade em SQLite.

## Portfólio de IA e automação

O ReportFlow é o projeto carro-chefe de um portfólio com nove módulos de operação logística. Os artefatos estão organizados em `data/`, `prompts/`, `workflows/` e `docs/`, com dados sintéticos, gabaritos e limitações explícitas.

| # | Projeto | Evidência entregue |
|---|---|---|
| 1 | Triagem de pedidos e e-mails | 40 casos, gabarito, prompt v1/v2 e workflow |
| 2 | Dashboard de desempenho logístico | 2.160 entregas e fórmulas OTIF/lead time |
| 3 | Alerta inteligente de estoque | 80 itens e cálculo de estoque de segurança |
| 4 | Inteligência de mercado | 20 notícias sintéticas e regra de fontes |
| 5 | Portal de solicitações e OKRs | 150 solicitações com SLA calculado |
| 6 | Auditoria de fatura de frete | 250 linhas e erros injetados |
| 7 | Assistente operacional | 40 perguntas com fonte e casos fora de escopo |
| 8 | Previsão de demanda e S&OP | 36 meses, 3 famílias e cenários |
| 9 | Torre de Controle ReportFlow | dashboard, exceções, aprovação humana e PDF |

O PDF de apresentação está em `docs/reportflow-case-study.pdf` e o roteiro de entrevista em `docs/interview-script.md`.

## Executar localmente

Requer apenas Python 3.10+ e Node.js 18+ (o Node é usado para os testes).

No Windows, abra `iniciar-reportflow.bat` com duplo clique. Ele inicia o backend, cria `reportflow.db` automaticamente e abre o navegador.

```bash
cd outputs/reportflow
python server.py
```

Abra `http://localhost:4173` no navegador. Para validar a lógica principal:

```bash
npm test
python -m unittest discover -s tests -p '*test.py' -v
```

## Fluxos disponíveis

- Dashboard com filtros de período, equipe e categoria, KPIs de vendas, custos, margem, produtividade e gráficos responsivos.
- Importação real de CSV e XLSX com validação e SQLite.
- Geração de PDF no backend e download pelo histórico.
- Automações diárias e semanais, logs e tentativas novamente.

## Arquitetura

Browser → Python API → SQLite, com Prisma e migração Supabase dedicados para evolução em produção. A IA propõe e explica; as regras calculam; ações de risco aguardam aprovação humana.
