# Justificativa das alterações do PR

Este documento explica o motivo de cada alteração realizada no pull request **“Atualiza laboratório com diretrizes e métricas do Copilot”**.

## Objetivo geral

O PR atualiza o hands-on para refletir o comportamento, a terminologia e as opções atuais do GitHub Copilot code review. Além de modernizar as instruções destinadas aos participantes, ele fortalece as validações automatizadas que verificam o progresso de cada etapa.

As alterações foram organizadas em quatro objetivos principais:

1. alinhar as instruções à interface atual do VS Code e do GitHub.com;
2. atualizar informações de cobrança, disponibilidade e capacidade do Copilot;
3. explicar corretamente instruções personalizadas, agent skills, MCP e a head branch;
4. tornar os workflows de validação mais precisos e úteis.

## `README.md`

### Atualização dos pré-requisitos

O pré-requisito genérico de uma “assinatura paga do GitHub Copilot” foi substituído por uma descrição mais precisa: acesso ao Copilot code review em um plano compatível, incluindo Copilot Pro, Pro+, Max, Business e Enterprise.

A alteração é necessária porque a disponibilidade do code review depende do plano e das políticas configuradas. Além disso, organizações com Copilot Business ou Enterprise podem habilitar o recurso para membros que não tenham uma licença individual, desde que as políticas apropriadas estejam ativadas.

### Inclusão de outros clientes compatíveis

Foi adicionada uma nota informando que o Copilot code review também está disponível em clientes como Visual Studio, JetBrains, Xcode, GitHub Mobile e GitHub CLI.

O exercício continua usando VS Code e GitHub.com, mas a informação ajuda o leitor a entender que o recurso faz parte de uma experiência mais ampla do GitHub Copilot.

## `.github/steps/1-step.md`

### Atualização do fluxo de revisão no VS Code

As instruções antigas orientavam o participante a abrir a paleta de comandos e procurar por `Chat: Review`. Elas foram atualizadas para o fluxo documentado no Source Control:

- abrir o painel **Source Control**;
- passar o mouse sobre **CHANGES**;
- selecionar **Copilot Code Review - Uncommitted Changes**.

Isso reduz a ambiguidade sobre qual comando deve ser utilizado e evita que o participante selecione uma funcionalidade diferente do code review.

### Inclusão da revisão de uma seleção de código

Foi adicionada uma alternativa para selecionar um trecho de código e usar **Generate Code > Review**.

Essa opção demonstra que o Copilot também pode revisar uma seleção específica, além de revisar todas as alterações não commitadas.

### Inclusão de arquivos excluídos

O passo passou a mencionar que arquivos como `*.lock`, `*.log`, `*.svg`, arquivos gerados e conteúdo de vendor podem ser excluídos da revisão.

Essa informação explica por que determinados arquivos podem não receber comentários do Copilot e evita que o participante interprete esse comportamento como falha do exercício.

### Melhoria do troubleshooting

A orientação de troubleshooting foi atualizada para mencionar diretamente o botão **Copilot Code Review - Uncommitted Changes**. Isso torna o diagnóstico mais objetivo quando o participante não receber feedback.

## `.github/steps/2-step.md`

### Atualização da terminologia de cobrança

O termo antigo **PRU** foi substituído por **AI credits**, alinhando o conteúdo à terminologia atual do GitHub Copilot.

Também foi documentado que os recursos agentic usados durante a revisão podem consumir **GitHub Actions minutes**. Isso é importante porque a revisão pode envolver coleta de contexto do projeto e uso de ferramentas em um ambiente de execução.

### Explicação dos níveis de esforço

Foi adicionada uma nota sobre os níveis **Low** e **Medium**:

- **Low** é o nível padrão e prioriza uma análise mais rápida;
- **Medium** realiza uma análise mais profunda e pode consumir mais AI credits e minutos do GitHub Actions.

Essa informação ajuda administradores e participantes a entenderem o equilíbrio entre profundidade, tempo e custo.

### Inclusão de arquivos excluídos

A etapa de revisão em pull requests agora informa que determinados arquivos, como locks, logs, SVGs e arquivos gerados, podem não ser analisados.

Isso mantém a explicação consistente com a etapa de revisão local no VS Code.

### Atualização da solicitação de revisão

A instrução que descrevia o uso de um ícone de configurações foi substituída pelo fluxo atual: localizar **Reviewers** e clicar em **Request** ao lado de **Copilot**.

A alteração torna o passo mais direto e alinhado à interface documentada do GitHub.com.

### Atualização da disponibilidade para membros sem licença

O troubleshooting deixou de afirmar que o recurso não está disponível no plano gratuito de forma genérica. Agora explica que políticas de organizações com Copilot Business ou Enterprise podem habilitar o code review para membros sem licença individual.

Isso evita uma orientação desatualizada e diferencia a disponibilidade por plano das políticas organizacionais.

## `.github/steps/3-step.md`

### Inclusão de instruções de agente

Foi adicionada a categoria de instruções de agente, com referência a `AGENTS.md`.

A alteração explica que esse arquivo pode fornecer contexto compartilhado para agentes e não apenas para o Copilot Chat em um cliente específico.

### Atualização dos exemplos de `applyTo`

Os padrões dos exemplos foram ampliados para usar caminhos recursivos, como:

- `**/*.test.*`;
- `docs/**/*.md`;
- `**/*.html`;
- `**/*.css`;
- `**/*.js`;
- `src/backend/**/*.py`.

Isso torna os exemplos mais úteis em repositórios com subdiretórios e faz com que as instruções alcancem os arquivos pretendidos em diferentes níveis da árvore.

### Documentação sobre a matriz de suporte

Foi adicionada uma nota informando que o suporte a cada tipo de instrução pode variar conforme o cliente, como GitHub.com, VS Code, Visual Studio, JetBrains, Xcode e CLI.

A ressalva evita que o participante presuma que todos os arquivos de instrução funcionam exatamente da mesma forma em todos os ambientes.

### Inclusão de `REVIEW.md`, `GEMINI.md` e `CLAUDE.md`

O conteúdo passou a mencionar formatos comuns de instruções mantidos na raiz do repositório.

Isso amplia o contexto apresentado no laboratório e mostra que o code review pode aproveitar diretrizes já existentes em arquivos utilizados por diferentes ferramentas de IA.

### Explicação sobre a head branch

Foi adicionada uma explicação importante: durante a revisão de um pull request, o Copilot lê as instruções, skills e arquivos relevantes a partir da branch de origem, ou **head branch**, e não da branch base.

Essa informação é essencial para o exercício porque permite testar alterações nas instruções dentro do próprio pull request, antes de mesclá-las.

### Atualização do padrão frontend

O padrão de frontend foi alterado para `**/*.html,**/*.css,**/*.js`, garantindo que as instruções sejam aplicadas aos arquivos correspondentes em subdiretórios.

### Atualização do padrão backend

O padrão de backend foi alterado para `src/backend/**/*.py`, refletindo a estrutura real do laboratório e evitando que a instrução seja aplicada de forma excessivamente ampla ou a arquivos fora do backend.

### Inclusão de `excludeAgent`

Foi adicionada uma orientação opcional sobre `excludeAgent`, permitindo explicar como uma instrução pode ser restringida a determinados tipos de agente, como code review ou cloud agent.

Isso apresenta uma capacidade avançada sem torná-la obrigatória para a conclusão do exercício.

### Clareza sobre a branch usada na re-revisão

As instruções agora pedem explicitamente que o participante faça commit e push das regras na branch `add-announcement-banner`, altere ou acrescente uma regra observável e solicite novamente a revisão no mesmo pull request.

A mudança transforma a ideia de “testar instruções” em uma atividade observável e demonstra na prática o uso das instruções presentes na head branch.

### Inclusão opcional de skills e MCP

Foi adicionada uma seção opcional sobre:

- agent skills em `.github/skills/`;
- servidores MCP configurados no repositório;
- `AGENTS.md` para regras compartilhadas.

A seção permite ampliar o laboratório para equipes que desejam conectar padrões internos e contexto externo às revisões, sem aumentar os pré-requisitos da atividade principal.

## `.github/steps/4-step.md`

### Correção conceitual sobre a revisão automática

O texto foi alterado de “exigir revisões do Copilot” para “solicitar automaticamente revisões do Copilot”.

Essa distinção é necessária porque o ruleset pode solicitar a revisão automaticamente, mas a revisão do Copilot é publicada como comentário. Ela não substitui uma aprovação humana obrigatória e não bloqueia o merge por si só.

Também foi explicado que um merge pode permanecer bloqueado por outras regras, como:

- exigir pull request;
- exigir aprovações humanas;
- exigir resolução de conversas.

### Atualização de cobrança

A etapa agora usa **AI credits** e informa que recursos agentic podem consumir **GitHub Actions minutes**, mantendo consistência com a Etapa 2.

### Inclusão da configuração automática individual

Foi adicionada uma nota informando que usuários em planos compatíveis também podem configurar revisões automáticas para os próprios pull requests nas configurações do Copilot.

Isso diferencia as configurações pessoais das regras aplicadas por repositórios e organizações.

### Inclusão de `Review new pushes`

A opção **Review new pushes** foi documentada como uma forma de solicitar novas revisões quando novos commits forem enviados ao pull request.

Isso esclarece por que um push posterior pode não gerar automaticamente uma nova revisão quando a opção não está habilitada.

### Inclusão de `Review draft pull requests`

A opção **Review draft pull requests** foi documentada para explicar que o Copilot pode revisar pull requests enquanto eles ainda estão em modo draft.

### Ajuste da descrição do botão de merge

A instrução deixou de afirmar que o botão de merge necessariamente ficará desabilitado. Agora informa que isso depende das demais regras habilitadas no ruleset.

Essa alteração evita atribuir ao code review do Copilot um comportamento de bloqueio que ele não possui isoladamente.

### Orientação responsável sobre comentários

O participante agora é instruído a revisar os comentários do Copilot e resolver apenas aqueles que foram tratados ou considerados não aplicáveis com justificativa.

Isso substitui a orientação anterior de resolver todos os comentários sem implementar nada e reforça que o feedback do Copilot deve ser validado por uma pessoa.

### Documentação sobre ambiente de execução

Foi adicionada uma nota sobre `.github/workflows/copilot-code-review.yml`, `copilot-setup-steps.yml`, runners e firewall.

A informação mostra como equipes podem personalizar o ambiente usado pelo code review em cenários que exigem dependências, desempenho ou restrições de rede específicas.

### Atualização da dica sobre modelos

A referência a modelos que usam PRUs foi removida. A nova versão explica que modelos mais avançados tendem a ser mais robustos, mas podem consumir mais AI credits.

## `.github/steps/x-review.md`

### Inclusão de métricas por repositório

Foi adicionada uma seção sobre os relatórios diários de métricas do Copilot em nível de repositório, incluindo os endpoints para organizações e enterprises.

A alteração amplia o resultado do laboratório: além de aprender a configurar revisões, administradores podem analisar adoção, participação e impacto do code review entre diferentes repositórios.

### Esclarecimento de acesso

O texto informa que a consulta depende da permissão **View Copilot Metrics** e que participantes comuns podem não ter acesso aos endpoints.

Isso evita que o hands-on apresente as métricas como disponíveis para qualquer usuário, independentemente das políticas da organização ou enterprise.

## `.github/workflows/2-step.yml`

### Ajuste do nome da validação

O passo foi renomeado de “Check if Copilot is assigned as reviewer” para “Check if Copilot review was requested”.

A nova descrição é mais precisa porque a atividade verifica a solicitação de revisão, não se o Copilot concluiu a análise ou forneceu comentários.

### Ajuste das mensagens e do resultado

As mensagens do shell e a descrição do resultado foram atualizadas para usar “review was requested”.

Isso mantém a validação coerente com o evento `review_requested` usado pelo workflow e evita afirmar que o pull request já foi revisado quando o workflow apenas confirmou a solicitação.

## `.github/workflows/3-step.yml`

### Validação da existência dos arquivos

O workflow continua validando a presença de:

- `.github/copilot-instructions.md`;
- `.github/instructions/frontend.instructions.md`;
- `.github/instructions/backend.instructions.md`.

Essas verificações garantem que o participante criou os arquivos exigidos pela atividade.

### Validação do front matter do frontend

Foi adicionada uma verificação que confirma:

- o delimitador inicial `---` na primeira linha;
- a presença de `applyTo:` dentro do bloco inicial;
- o delimitador de fechamento `---`.

A validação é executada somente quando o arquivo existe. A expressão `awk` foi ajustada para retornar sucesso corretamente quando o front matter é válido.

### Validação do front matter do backend

A mesma lógica foi aplicada ao arquivo de backend, incluindo a condição que impede a execução da checagem quando o arquivo não existe.

Isso evita falsos positivos causados por ocorrências de `---` ou `applyTo:` no corpo do Markdown e produz um resultado separado para a configuração do backend.

### Atualização do relatório de resultados

O relatório da Etapa 3 agora diferencia:

- criação do arquivo geral;
- criação do arquivo de frontend;
- validade do front matter do frontend;
- criação do arquivo de backend;
- validade do front matter do backend.

Essa granularidade torna o feedback mais útil para o participante, pois indica exatamente qual parte da configuração precisa ser corrigida.

## `.github/workflows/4-step.yml`

### Remoção da limitação a repositórios públicos

A condição que executava a validação de rulesets apenas em repositórios públicos foi removida.

A consulta passou a ser tentada também em repositórios privados, desde que o token tenha permissões adequadas. Isso torna o workflow compatível com mais cenários de uso.

### Tratamento explícito de erros da API

A checagem agora captura a saída padrão e o erro separadamente. Com isso, é possível diferenciar:

- falha de autenticação;
- falta de permissão;
- falha genérica da API;
- resposta JSON inválida;
- ausência de rulesets ativos;
- ausência da regra automática do Copilot.

Essa alteração evita que uma falha de acesso seja apresentada incorretamente como ausência de configuração.

### Validação da resposta JSON

Antes de processar os dados, o workflow confirma que a listagem de rulesets é um array JSON e que cada detalhe de ruleset é um objeto JSON.

Isso evita erros silenciosos ou resultados incorretos quando a API retornar um formato inesperado.

### Verificação de rulesets ativos

A validação filtra apenas rulesets com enforcement ativo, pois o objetivo do exercício é confirmar uma regra realmente aplicada ao repositório.

### Verificação da regra de revisão do Copilot

Em vez de procurar apenas palavras no nome do ruleset, o workflow consulta os detalhes de cada ruleset e procura uma regra do tipo `copilot_code_review`.

Essa abordagem é mais precisa porque valida a regra configurada, não apenas o nome escolhido pelo participante.

### Mensagens acionáveis

Foram adicionadas mensagens específicas para autenticação, permissões, JSON inválido e configuração ausente.

Isso reduz o tempo de diagnóstico e ajuda o participante ou administrador a corrigir o problema correto.

### Atualização do relatório da Etapa 4

A descrição do resultado passou a indicar que o repositório possui um ruleset ativo com solicitação automática de revisão do Copilot.

Essa mensagem corresponde melhor ao que o workflow realmente verifica.

## Conclusão

As alterações tornam o hands-on mais atualizado, preciso e confiável. A documentação agora diferencia solicitação automática de revisão de aprovação obrigatória, explica os custos e níveis de esforço, apresenta os mecanismos de personalização disponíveis e orienta corretamente sobre a origem das instruções.

Os workflows também passaram a validar não apenas a existência dos arquivos, mas a configuração efetiva do front matter e da regra de revisão automática, com mensagens mais úteis para diagnóstico.
