## Etapa 4: Automatize as Revisões


As revisões personalizadas parecem estar funcionando muito bem, mas há um problema: elas não são tecnicamente obrigatórias. Solicitar revisões do Copilot manualmente não é sustentável quando há vários professores contribuindo para o site de atividades. Você quer que todo pull request receba automaticamente o feedback do Copilot, especialmente porque há diferentes níveis de experiência em programação entre os colaboradores. Vamos configurar regras do repositório para **solicitar automaticamente** revisões do Copilot em todas as mudanças.

### 📖 Teoria: Regras de Repositório para Revisões Automáticas


As regras do repositório permitem configurar revisões automáticas de código em pull requests, garantindo verificações de qualidade consistentes sem depender dos desenvolvedores para solicitar revisões manualmente ou lembrar de seguir a documentação.


Quando você ativa **Automatically request Copilot code review**, o Copilot passa a ser solicitado automaticamente e publica a revisão como comentário no pull request. Essa revisão **não substitui aprovação humana obrigatória** e **não bloqueia merge por si só**. Se o merge ficar bloqueado, o motivo será outra regra do ruleset (por exemplo: exigir pull request, aprovações humanas ou resolução de conversas).


Cada revisão de código consome **AI credits**. Além disso, recursos agentic da revisão podem consumir **GitHub Actions minutes**.


**Opções de Aplicação:**


- **Nível de repositório**: Todos os novos pull requests no repositório específico
- **Nível de branch**: Direciona branches específicas por filtros e padrões de nome
- **Nível de organização**: Aplica regras em múltiplos repositórios


**Principais Benefícios:**


- Qualidade de código consistente em todas as contribuições
- Aplicação automática sem intervenção manual
- Configurável conforme as necessidades de proteção de branch
- Integração com as permissões do fluxo de trabalho do GitHub


Para mais informações, veja a [documentação de regras de repositório](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets).

> [!NOTE]
> Além de rulesets no repositório/organização, usuários individuais em planos compatíveis também podem habilitar revisão automática para seus próprios pull requests nas configurações do Copilot.

### ⌨️ Atividade: Crie uma regra de repositório


1. No menu superior, selecione a aba **Settings**.


2. No menu à esquerda, expanda **Rules** e selecione **Rulesets**.


3. Clique no botão **New ruleset** e selecione a opção **New branch ruleset**.


4. Defina o nome e o status da regra:


   - **Ruleset Name**: `Require Copilot Reviews`
   - **Enforcement Status**: `Active`


5. Em **Target branches**, adicione proteções para a branch `main`.
   

   - Clique em **Add target** e **Include default branch**.
   - Clique em **Add target** e **Include by pattern**.
   - Digite `main` e clique em **Add inclusion pattern**.


   <img width="300" alt="screenshot of target branches" src="https://github.com/user-attachments/assets/217f205c-7a61-4ffa-a0a6-7e76ff8d7906"/>


6. Em **Rules**, habilite as opções abaixo:


   - **Exigir pull request antes de mesclar**: ☑️
   - **Exigir resolução de conversas antes de mesclar**: ☑️
   - **Solicitar automaticamente revisão de código do Copilot**: ☑️
   - (Opcional) **Review new pushes**: ☑️
   - (Opcional) **Review draft pull requests**: ☑️

   **Sobre as opções opcionais:**
   - **Review new pushes**: solicita nova revisão automática quando novos commits são enviados ao pull request.
   - **Review draft pull requests**: permite que a revisão automática também aconteça enquanto o pull request ainda está em draft.
   - Se essas opções não forem habilitadas, a revisão automática não necessariamente será executada novamente a cada push ou durante a fase de draft.


7. Role até o final e clique em **Create**.


8. Volte para o pull request aberto.


9. Dependendo das demais regras habilitadas no ruleset, o botão de merge pode ficar desabilitado até que os requisitos sejam atendidos.

   <img width="300" alt="screenshot of disabled merge button" src="https://github.com/user-attachments/assets/28e4cb05-f09d-423d-8c77-8f0ec61c73ad"/>


10. Revise os comentários do Copilot com cuidado. Resolva apenas os que realmente foram tratados (ou considerados não aplicáveis com justificativa).


11. Faça o merge do pull request.


> [!NOTE]
> Se o botão **Merge pull request** não ativar, verifique se há conversas não resolvidas nos comentários antigos.

> [!NOTE]
> Em ambientes com requisitos de rede ou performance, você pode personalizar a execução da revisão com `.github/workflows/copilot-code-review.yml` (ou `copilot-setup-steps.yml`), definir runners e ajustar regras de firewall.


12. Com o pull request mesclado, aguarde um momento para a Mona checar seu trabalho, fornecer feedback e fazer a revisão final. Parabéns! Você terminou! 🎉

### ⌨️ Atividade: (opcional) Teste revisões automáticas


Ainda não quer terminar? Está incomodado com o banner de anúncio hard coded? Nós também!


Então... vamos corrigir isso! 🧑‍🚀🚀



> [!NOTE]
> Você não precisa "corrigir" o novo recurso de Anúncio. Se quiser apenas testar as revisões automáticas, basta fazer uma pequena alteração e abrir um novo pull request.


13. No VS Code, volte para a branch `main`, puxe as alterações mescladas e exclua a branch `add-announcement-banner`.


14. Crie uma nova branch a partir da `main` com o nome abaixo.

   ```txt
   enable-editing-announcements
   ```


15. Abra o painel do Copilot Chat e certifique-se de que está no **modo Agent**. Use o prompt abaixo para pedir ao Copilot que melhore o novo recurso de Anúncios.


> [!TIP]
> Modelos mais avançados normalmente são mais robustos e exigem menos prompts de refinamento, porém tendem a consumir mais AI credits.


   > ![Static Badge](https://img.shields.io/badge/-Prompt-text?style=social&logo=github%20copilot)
   >
   > ```prompt
   > O recurso de Anúncio não deve ser hard coded.
   >
   > - Faça com que seja alimentado pelo banco de dados.
   > - Adicione um botão no cabeçalho que abre uma janela de diálogo. Ela lista todos os anúncios existentes e tem controles para adicionar/modificar/excluir.
   > - Apenas usuários logados podem gerenciar anúncios.
   > - Anúncios exigem data de expiração. Data de início é opcional.
   > - Adicione uma mensagem de exemplo na inicialização do banco de dados.
   > - Não se preocupe com testes unitários.
   > - Capriche na experiência de UI/UX.
   > ```

16. (opcional) Rode a aplicação para testar as mudanças e forneça prompts adicionais ao Copilot para refinar ainda mais.

17. (opcional) Antes de fazer commit das mudanças, peça uma revisão local no VS Code.

18. Faça commit e push das alterações.

19. Crie um novo Pull Request com os seguintes detalhes.

   - **compare:** `enable-editing-announcements`
   - **target:** `main`
   - **title:** `Enable Editing Announcements`

20. Note que o Copilot foi adicionado automaticamente como revisor. Aguarde um momento pelo feedback.

21. (opcional) Resolva quaisquer comentários do Copilot.

22. Faça o merge do pull request.

23. Muito bom! Você terminou tudo, de novo! 🎉
