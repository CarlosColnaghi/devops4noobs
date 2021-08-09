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

## Principais Comandos

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

### Unir branchs com merge

    $ git merge nome_da_branch

### Unir banchs com rebase

    $ git rebase nome_da_branch

## GITIGNORE
É um arquivo que determina os arquivos que serão ignorados no processo de versionamento

## STASH
É um comando para armazenar temporariamente as mudanças de arquivos que estão no estado modified

### Armazenar as mudanças na lista
    $ git stash

### Recuperar e aplicar as mudanças lista

    $ git stash apply

### Limpar a lista de mudanças

    $ git stash clear

### Listar as mudanças da lista

    $ git stash list

## TAGS
São marcações que representam uma versão da release do projeto

## Comandos

### Criar uma tag
    $ git tag -a versao -m "mensagem"

### Listar as tags
    $ git tag

### Enviar as tags para os repositórios remotos
    
    $ git push origin master --tags

## REVERT

É uma maneira de criar um novo commit para voltar para uma versão anterior

## Comandos

### Reverter um commit
    $ git revert endereco_do_commit


# AWS

## Serviços

- EC2
- VPC
- Route 53
- S3
- Cloud Watch
- IAM

## AWS CLI
1.  Criar um novo grupo de administradores
    - Group Name: nome_do_grupo
    - Attach Policy: AdministratorAccess

2. Adicionar um novo usuario
    - User name: nome_do_usuario
    - Acess type: [x] Programatic access
    - Add user to group: [x] nome_do_grupo

### Comandos
Iniciar o processo de configuração do AWS CLI

    $ aws configure

### Configuração

    AWS Access Key ID: *******
    AWS Secret Access Key: *******
    Default region name: us-east-1
    Default output format: json

## EC2 (Elastic Compute Cloud)

### Conteúdos
- Instâncias (virtualização de máquinas e servidores)
- Balanceamento de Carga (Load Balance)
- Escalonamento (AWS Auto Scaling)
- Armazenamento
- Segurança (keys)

### Regiões, Zonas de Disponibilidade e Zonas Locais

Cada região é composta por pelo menos três data centers que representam as zonas de disponibilidades (AZ). Já as zonas locais se conectam a uma ou mais zonas de disponibilidade para diminuir a latência

- Direct Connect: conexão entre uma zona local e o cliente
- Backbone: conexão entre uma zona local e uma zona de disponibilidaade

### Tipos de instâncias EC2

- Uso geral
- Otimizadas para CPU
- Otimizadas para RAM
- GPU
- Otimizadas para Armazenamento

### Criar instâncias EC2

1. Launch Instance: Inicia o processo de criação das instâncias

2. Choose an Amazon Machine Image (AMI): Determina a imagem do sistema operacional da instância

3. Choose an Instance Type: Determina o tipo de instância (principalmente com relação ao hardware)

4. Configure Security Group: Permite criar um novo grupo com os padrões para acessar a instância

5. Create a new key pair: Cria um par de chaves para acessar a instância via SSH

### Configure Instance Details
- Number of instances: determinquantidade de instâncias
- Shutdown behavior: comportamento executado no momento que a máquina é desligada
    - Terminate: impede que a máquina seja inicializada novamente depois de desligada (em outras palavras, a instância é terminada)
    - Stop: permite que a máquia seja inicializada novamente depois de desligada
- Termination protection: protege contra o desligamento "acidental" de uma máquina

### Mudar a permissão de uma chave SSH 
É importante que apenas o dono tenha a permissão de realizar a leitura da chave

    $ chmod 400 caminho_da_chave

### Conectar com uma instância EC2

    $ ssh -i caminho_da_chave nome_do_usuario@endereco_da_instancia

### Comandos

Listar todas as instâncias 
    
    $ aws ec2 describe-instances

Remover uma instância

    $ aws ec2 terminate-instances --instance-ids "id-xyz"

Exemplo de parâmetros para criar uma instância 

    $ aws ec2 run-instances --image-id "ami-0323c3dd2da7fb37d" --count 1 --instance-type "t2.micro" --key-name "MinhaChaveSSH" --security-group-ids "sg-0529062a5d07f7eab" --subnet-id "subnet-1deb2d3c

### AMI
- Uma AMI é uma imagem de uma máquina e uma instância sempre está associada à uma AMI
- Por padrão, uma AMI é privada e reservada para a sua região de origem
- A AMI é armazenada pelo serviço de Bucket
- É possível criar uma instância com base em AMI e depois de customizar essa instância, ainda é possivel criar uma nova AMI com base na instância customizada

- Tipos de AMI
    - Região
    - Sistema Operacional
    - Arquitetura
    - Permissões de execução (pública, explícita e implícita)
    - Armazenamento

### Customização em tempo de execução de uma AMI

1. Advances Details
    - User data: [x] As text
    
            $ #!/bin/bash

            $ yum update -y
            $ yum install httpd -y
            $ systemctl start httpd
            $ systemctl enable 
