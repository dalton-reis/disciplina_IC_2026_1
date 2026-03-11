# Material Didático: Git e GitHub – Do Básico ao Avançado

Este material foi estruturado para fornecer uma compreensão progressiva do controle de versão, desde a configuração inicial até fluxos de colaboração profissionais utilizando o Git (tecnologia) e o GitHub (produto).

--------------------------------------------------------------------------------

## Introdução ao Controle de Versão

O Git é um Sistema de Controle de Versão Distribuído (DVCS) gratuito (pago para grande quantidade de uso) e de código aberto, projetado para lidar com projetos de todos os tamanhos com velocidade e eficiência. Ao contrário de sistemas antigos que armazenam informações como uma série de mudanças em arquivos (deltas), o Git trata os dados como um conjunto de "snapshots" (fotos) do estado do projeto em um determinado momento.
Por que usar o Git?

- Velocidade e Eficiência: quase todas as operações são locais, o que as torna quase instantâneas.
- Integridade: tudo no Git passa por uma soma de verificação (checksum) SHA-1 antes de ser armazenado, tornando impossível alterar arquivos sem que o sistema detecte.
- Trabalho Offline: como você possui uma cópia completa do repositório em sua máquina, pode trabalhar sem conexão de rede e sincronizar depois.

--------------------------------------------------------------------------------

## Configuração Inicial e Identidade

Antes de começar a usar o Git, é essencial configurar sua identidade. Essas informações são gravadas de forma imutável em cada `commit` que você cria.

### Comandos de Configuração Global

Use o comando `git config` para definir suas preferências:

| Objetivo | Comando |
| -- | -- |
| Definir Nome | `git config --global user.name "Seu Nome"` |
| Definir E-mail | `git config --global user.email "seuemail@exemplo.com"` |
| Listar Configurações | `git config --list` |
<!-- | Definir Editor Padrão | `git config --global core.editor emacs` | -->

> [!IMPORTANT]  
> A configuração do e-mail é crucial no GitHub, pois é através dela que a plataforma mapeia seus *commits* para o seu perfil de usuário.

--------------------------------------------------------------------------------

## Fundamentos do Fluxo de Trabalho Local

Para entender o Git, você deve dominar o conceito dos Três Estados em que um arquivo pode residir.

Os Três Estados e Áreas do Git:

- Diretório de Trabalho (Working Directory): onde você modifica os arquivos localmente.
- Área de Preparo (Staging Area/Index): onde você marca os arquivos modificados para fazerem parte do próximo `commit`.
- Diretório Git (History): onde o Git armazena permanentemente os snapshots no banco de dados.

Sequência Básica de Comandos:

- git init: cria um novo repositório Git em um diretório existente.
- git status: mostra o estado atual dos arquivos (quais foram modificados, preparados ou não rastreados).
- git add <arquivo>: Move as alterações do diretório de trabalho para a área de preparo.
- git commit -m "mensagem": Grava o snapshot da área de preparo permanentemente no histórico.

> [!TIP]
> Boas mensagens de commit devem ser curtas (cerca de 50 caracteres), descrever a mudança no imperativo e contar a história da evolução do projeto.

--------------------------------------------------------------------------------

## Trabalhando com Repositórios Remotos e GitHub

O GitHub é uma plataforma de colaboração construída sobre o Git, focada em facilitar o compartilhamento de código e o trabalho em equipe.

Sincronização de Projetos:

- Clonagem (git clone): cria uma cópia local de um repositório remoto, incluindo todo o seu histórico.
- Busca (git fetch): baixa os dados do servidor remoto para o seu banco de dados local, mas não mescla automaticamente com seu trabalho atual.
- Atualização (git pull): Combina os comandos fetch e merge, baixando os dados e tentando integrá-los ao seu branch atual.
- Envio (git push): envia seus commits locais para o servidor remoto.

### Fluxo de Colaboração do GitHub (GitHub Flow)

Este fluxo permite experimentar ideias com segurança:

- Fork: crie sua própria cópia do projeto no seu namespace no GitHub.
- Branch: crie um branch para suas alterações.
- Commit: faça alterações e grave os snapshots.
- Pull Request: abra uma solicitação para que o proprietário do projeto original revise e aceite suas mudanças.

--------------------------------------------------------------------------------

## Ramificações (Branches) e Integração

O modelo de ramificação é considerado o "recurso matador" do Git por ser incrivelmente leve e quase instantâneo.

Gestão de Branches:

- Criar Branch: `git branch <nome-da-branch>`
- Trocar de Branch: `git checkout <nome-da-branch>`
- Mesclar (Merge): integra o histórico de um branch em outro

### Comparativo de Integração: Merge vs. Rebase

Existem duas formas principais de integrar mudanças entre branches:
| Método | Funcionamento | Resultado no Histórico |
| -- | -- | -- |
| Merge | Realiza uma mesclagem de três vias entre os snapshots e cria um novo "commit de merge" | Preserva o histórico real de como e quando as coisas aconteceram |
| Rebase | Pega as mudanças introduzidas em um branch e as "reaplica" no topo de outro | Cria um histórico linear, como se o trabalho tivesse ocorrido em série |

> [!WARNING]
> Regra de Ouro do Rebase: Nunca faça rebase de commits que você já enviou para um repositório público, pois isso reescreve a história e causará problemas para seus colaboradores.

--------------------------------------------------------------------------------

## Recursos Avançados de Organização

### Tags e Releases

As Tags são usadas para marcar pontos importantes na história, como lançamentos de versões (v1.0, v2.0):

- Anotadas: contêm o nome do autor, e-mail, data e mensagem (recomendado).
- Leves: funcionam apenas como um ponteiro que não muda para um commit específico.

### Ignorando Arquivos com .gitignore

Arquivos gerados automaticamente (logs, binários, configurações locais) não devem ser rastreados. Liste os padrões no arquivo .gitignore para que o Git os ignore.

### Atalhos (Aliases)

Você pode criar atalhos para comandos longos para aumentar a produtividade:

`git config --global alias.st status` (agora você pode usar git st).
`git config --global alias.unstage` 'reset HEAD --'.
