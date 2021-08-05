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
    $ git add nome_do_arquivo

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

### Sincronizar um repositório local com o repositório no Github

    $ git remote add origin endereco_do_repositorio
    $ git push -u origin main

### Enviar os commits de um repositório local para o repositório no Gihub

    $ git push origin main


## CLONE X FORK

O clone é usado quando o dono do repositório é o próprio usuário, enquanto que o fork é o contrário, e portanto, deve ser usado quando o usuário não é o dono de repositório.

## BRANCHES

São ponteiros associados aos commits que permitem criar "cópias" do repositório para o desenvolvimento paralelo sobre o mesmo projeto

### Comandos

### Clonar um repositório próprio
    $ git clone endereco_do_repositorio


### Criar uma nova branch
    $ git checkout -b nome_da_branch

### Listar todas as branchs
    $ git branch

### Deletar uma branch
    $ git branch -D nome_da_branch

### Mudar para uma outra branch
    $ git checkout nome_da_branch

## MERGE X REBASE
Tanto o merge quanto rebase são métodos para unir os commits das branchs. O merge é uma operação não destrutiva, no entanto, depende de um novo commit que aponta para os commits de outras branchs. Em contrapartida, o rebase move os commits de uma branch para "frente" da sequência de commits de uma outra branch.

## Comandos

