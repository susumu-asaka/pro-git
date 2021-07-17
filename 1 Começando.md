## 1 Começando

### 1.1 Sobre Controle de Versão

#### Sistemas Locais de Controle de Versão

![Figura 1. Controle de versão local.](C:\Users\Semantix\Pro Git\local.png)

#### Sistemas Centralizados de Controle de Versão

![Figura 2. Controle de versão centralizado](C:\Users\Semantix\Pro Git\centralized.png)

#### Sistemas Distribuídos de Controle de Versão

![Figura 3. Controle de versão distribuídos](C:\Users\Semantix\Pro Git\distributed.png)

### 1.2 Uma Breve História do Git

Algumas metas do novo sistema:

* Velocidade
* Design simples
* Forte suporte para desenvolvimento não-linear (milhares de ramos paralelos)
* Completamente distribuído
* Capaz de lidar com projetos grandes como o kernel de Linux com eficiência (velocidade e tamanho dos dados)

### 1.3 O Básico do Git

#### Deltas

![Figure 4. Armazenando dados como alterações em versão básica de cada arquivo.](C:\Users\Semantix\Pro Git\deltas.png)

#### Snapshots

![Figura 5. Armazenando dados como um estado do conjunto de arquivos do projeto ao longo do tempo](C:\Users\Semantix\Pro Git\snapshots.png)

#### Quase Todas as Operações são Locais

#### Git Tem Integridade

```bash
24b9da6552252987aa493b52f8696cd6d3b00373
```

#### O Git Geralmente Somente Adiciona Dados

#### Os Três Estados

![Figure 6. Diretório de trabalho, área de preparo, o diretório Git.](C:\Users\Semantix\Pro Git\areas.png)

Fluxo de trabalho básico Git:

1. Você modifica arquivos no seu diretório de trabalho.
2. Você prepara os arquivos, adicionando retratos deles à sua staging area.
3. Você faz `commit`, que leva os arquivos como eles estão na staging area e armazena esses retratos de forma permanente para o diretório do Git.

### 1.4 A Linha de Comando

### 1.5 Instalando o Git

#### Instalando no Linux

Se usar Fedora, por exemplo, pode usar yum:

```bash
$ sudo yum install git-all
```
Se usar uma distribuição baseada em Debian, como o Ubuntu, use o apt-get:
```bash
$ sudo apt-get install git-all
```

#### Instalando no Mac

Um instalador OSX Git é mantido e disponível para download no site do Git, pelo http://git-scm.com/download/mac.

#### Instalando no Windows

A compilação oficial está disponível no site do Git, pelo http://git-scm.com/download/win.

#### Instalando da Fonte

### 1.6 Configuração Inicial do Git

Os parâmetros de configuração podem ser armazenados em três lugares diferentes:

1. `/etc/gitconfig`: válido para todos os usuários no sistema e todos os seus repositórios. Se você passar a opção `--system` para `git config`, ele lê e escreve neste arquivo.
2. `~/.gitconfig` ou `~/.config/git/config`: Somente para o seu usuário. Você pode fazer o Git ler e escrever neste arquivo passando a opção `--global`.
3. `config` no diretório Git (ou seja, `.git/config`) de qualquer repositório que você esteja usando: específico para este repositório.

#### Sua Identidade

```bash
$ git config --global user.name "Fulano de Tal"
$ git config --global user.email fulanodetal@exemplo.com
```

#### Seu Editor

```bash
$ git config --global core.editor code
```

### Verificando Suas Configurações

```bash
$ git config --list
user.name=Fulano de Tal
user.email=fulanodetal@exemplo.br
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
...
```

```bash
$ git config user.name
```

### 1.7 Pedindo Ajuda

```bash
$ git help <comando>
$ git <comando> --help
```

```bash
$ git help config
```

### 1.8 Resumo

Você deve ter um entendimento básico do que o Git é e como ele é diferente de sistemas de controle de versão centralizados que você talvez tenha usado anteriormente. 

Você já deve ter também uma versão do Git funcionando na sua máquina que está configurada com o seu toque pessoal. 

Agora é hora de começar a aprender o básico sobre Git.

