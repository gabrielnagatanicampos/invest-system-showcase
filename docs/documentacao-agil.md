# Invest System: documentação ágil (resumo)

Resumo do relatório entregue no fim da Sprint 2 (24/11), em versão pública. Depois dele, as funções da Sprint 2 (login, importação de CSV, assistente da carteira, banco online e alertas por e-mail) foram publicadas e estão no ar. O projeto é meu e já existia antes da disciplina de Métodos Ágeis (UMC); nela, trabalhamos em dupla, eu como Product Owner e um colega como Scrum Master do time.

## Problema e público

**Público.** Quem investe por conta própria em ações e criptomoedas e quer manter a carteira nas proporções planejadas, principalmente quem está começando.

**Problema.** Os preços mudam todo dia e alguns ativos passam a pesar mais ou menos do que a meta. Calcular quanto comprar ou vender exige planilha e conta manual. Quem não alcança o valor mínimo das gestoras acaba fazendo isso sozinho.

**Função principal.** Calcular, com cotações do dia, quanto comprar ou vender de cada ativo para a carteira voltar às metas.

## Backlog de histórias

| # | História (resumo) | Critérios de aceite principais | Pontos | Sprint |
|---|---|---|---|---|
| 1 | Ver quanto comprar ou vender de cada ativo | Diferença entre valor ideal e saldo atual; positivo é comprar, negativo é vender; avisa se as metas não somam 100% | 5 | 1 |
| 2 | Todo ativo com cotação | Ticker válido traz o último fechamento; sem cotação, aviso com o nome e fora do cálculo; app não quebra | 3 | 1 |
| 3 | Abrir por link público | App abre sem instalar nada; nenhuma senha ou chave no repositório; README explica | 5 | 1 |
| 4 | Entrar com conta e ver só a minha carteira | Recusa usuário repetido e senha curta; senha guardada com hash; dois usuários não veem a carteira um do outro | 3 | 2 |
| 5 | Importar carteira por CSV | Colunas ticker e quantidade; linhas inválidas listadas e as válidas entram; CSV de exemplo fictício | 5 | 2 |
| 6 | Assistente lê a carteira e explica a concentração | Recebe tickers e participação; explica sem recomendar compra nem venda; se o provedor cair, o resto do app segue | 5 | 2 |
| 7 | Assistente compara duas empresas | Comparação em português claro; aviso de que não é recomendação; pergunta fora do tema é recusada com educação | 3 | 3 |
| 8 | Baixar o resultado em CSV | Arquivo com ativo, saldo, valor ideal e diferença; abre no Excel com acentos corretos | 3 | 3 |
| 9 | Carteira salva em banco online | Dados continuam lá depois de reiniciar; conexão por variável de ambiente; testes com dados fictícios | 5 | 2 |
| 10 | E-mail quando a carteira precisar de atenção | Limite de desvio de 5 pontos percentuais, configurável; e-mail lista o que comprar ou vender; falha no envio não derruba o painel | 5 | 2 |

Uma história que falhou no critério INVEST: "assistente que analisa a carteira, compara empresas e explica tudo" era grande demais para uma sprint e impossível de estimar. Dividimos em duas (6 e 7).

## Definition of Ready e Definition of Done

| Definition of Ready | Definition of Done |
|---|---|
| História no formato Como, quero, para | Critérios de aceite cumpridos e mostrados na Review |
| Critérios que se respondem com sim ou não | Testes automáticos passando, inclusive os do código escrito com IA |
| Pontuada na Planning | Pull Request revisado pelo outro integrante e integrado na main |
| Cabe em uma sprint e não depende de outra história pendente | Publicada no link do projeto |
| Dados e acessos definidos | Sem senha ou chave no repositório, README atualizado, uso de IA registrado |

## Política do quadro

| Coluna | Limite | Regra para entrar |
|---|---|---|
| A fazer (Sprint) | sem limite | Cumpre a Definition of Ready e foi escolhida na Planning |
| Em desenvolvimento | 2 | A pessoa puxa a história e coloca o próprio nome; no máximo uma por pessoa |
| Em revisão | 1 | Pull Request aberto e testes passando; quem escreveu não aprova o próprio |
| Em validação no ar | 1 | Aprovada e integrada; o time confere os critérios no link publicado |
| Pronto | sem limite | Critérios cumpridos e Definition of Done completa |

Retrospectiva da Sprint 1 (Começar, Parar, Continuar): abrir o Pull Request de cada história no dia em que o código fica pronto, em vez de juntar tudo no fim da sprint.

## XP e entrega

- **Testes automáticos.** 285 testes passam, 1 é pulado (exige um servidor PostgreSQL) e 1 é esperado a falhar (metas que não somam 100% ainda não são recusadas). Foram gerados com apoio de IA e revisados por mim.
- **Integração contínua.** Cada história em uma branch própria; as verificações rodam a cada alteração e Pull Request.
- **Entrega.** Entrega contínua: a main fica pronta para publicar e uma pessoa do time publica com um comando. Trocamos a hospedagem gratuita inicial por uma VPS, por sugestão do professor, porque ela não guarda banco de dados nem roda o envio de alertas.
- **HTTPS.** Configurado, certificado ainda não emitido.
- **Publicação automática.** Pendente.
- **Teste por alguém de fora.** Uma colega abriu o app pelo link e funcionou. Faltou registrar se ela rebalanceou uma carteira, então entra na próxima sprint.

## Uso responsável de IA

Regra do time: o código escrito com IA deve entrar por Pull Request revisado por outro integrante e só seguir se passar nos testes (na Sprint 2 os Pull Requests ainda não tinham sido abertos). Cada pessoa precisa saber explicar o que entrou.

| Erro da IA | O que eu fiz |
|---|---|
| Hipóteses sobre ativos sem preço que os dados não provavam | Mantive só o que foi conferido: o código novo tem preço |
| Arquivo de configuração do Git próprio que conflitava com o do projeto | Descartei |
| Tipo de número do banco que voltaria em formato errado e quebraria as contas | Troquei por outro tipo |
| Formulário de cadastro que sumia ao digitar | Corrigi, criei um teste que falha nesse caso e validei no navegador |
| Quantidade do CSV sem limite máximo | A importação passou a recusar valores acima do limite do banco |
| Chat que respondia erro até para "oi", porque a integração só tinha sido testada com cliente simulado | Corrigi e passamos a exigir ao menos uma chamada real antes de aprovar |
| Preço zero podia causar divisão por zero no cálculo de variação | Corrigi |
| Três tarefas em paralelo partiram de uma base antiga | Refiz a partir da base certa |

## Próximos passos

1. Passar cada função da Sprint 2 pela Definition of Done.
2. Verificar o banco PostgreSQL.
3. Emitir o certificado HTTPS (precisa de domínio).
4. Publicação automática a cada alteração na main.
5. Novo teste com alguém de fora, cobrindo o rebalanceamento.
