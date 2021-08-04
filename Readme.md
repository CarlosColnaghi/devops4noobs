# devops4noobs

## Conteúdos

- git e github
- aws
- docker
- linux
- kubernets

# Git e Github

## Conceitos

- Controle de versão (gerenciamento de versões de um documento)
- Snapshot dos estados dos documentos (versão)
- Desenvolvimento não linear (brachs em paralelo)
- Github é diferente de Git. O Github é um serviço para armazenamento dos projetos versionados em Git

## Estados dos arquivos
- <b>untracked:</b> o arquivo que não esta sendo versionado
- <b>unmodified:</b> o arquivo esta sendo versionado, mas não tem mudanças
- <b>modified:</b> o arquivo mudou em relação a versão anterior, mas não esta preparado para entrar na próxima versão 
- <b>staged:</b> o arquivo esta preparado para um commit (versão do repositório ou snapshot dos arquivos)

## Comandos

### Configurações de variáveis de usuários

    $ git config --global user.name "Nome"
    $ git config --global user.email "email@email.com"

### Consultar os valores das variáveis usuarios

    $ git config user.name
    $ git config user.email

### Consultar uma lista com os valores de tovas as  variáveis
    $ git config --list

### Iniciar o versionamento de um repositório

    $ git init

### Consultar o estado do repositório

    $ git status

### Adicionar os arquivos para o estado de versionamento
    $ git add {nome do arquivo}

### Criar um commit
    $ git commit -m "mensagem"

### Criar um commit e ao mesmo tempo adicionar os arquivos para o estado de versionamento
    $ git commit -am "mensagem"

### Consultar logs
    $ git log
    $ git log --author="Nome"
    $ git shortlog 
    $ git shortlog -sn
    $ git log --graph

### Consultar dados de um commit
    $ git show identificador_do_commit

### Consultar o que mudou em arquivos modified
    $ git diff
    $ git diff --name-only

### Resetar mudanças de arquivos no estado modified
    $ git checkout nome_do_arquivo


### Resetar os novos arquivos adicionados para o versionamento
    $ git rm --chached nome_do_arquivo

### Resetar o estado dos arquivos de staged para modified
    $ git reset HEAD nome_do_arquivo

### Resetar os arquivos para um commit anterior, mas os arquivos retornam para o estado staged
    $ git reset --soft identificador_do_commit_anterior

### Resetar os arquivos para um commit anterior, mas os arquivos retornam para o estado modified
    $ git reset --mixed identificador_do_commit_anterior

### Resetar os arquivos para um commit anterior, mas os arquivos retornam para o estado unmodified
    $ git reset --hard identificador_do_commit_anterior