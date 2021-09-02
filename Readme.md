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
    - Acess type: Selecionar "Programatic access"
    - Add user to group: Selecionar "nome_do_grupo"

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

### Customizar em tempo de execução de uma AMI
1. Instances

2. Launch Intance

3. Configure Instance Details
    - Advanced Details
        - Em User Data é possível inserir um script que será exacutado durante o deploy da instância
        - User data: Selecionar "As text"
            
                $ #!/bin/bash

                $ yum update -y
                $ yum install httpd -y
                $ systemctl start httpd
                $ systemctl enable 

### Liberar portas dos grupos de segurança
1. Inbound rules
2. Edit inbound rules
3. Add rule
5. Save rule

### Indenficar se um serviço esta rodando no EC2

    $ rpm -qa | grep httpd
    $ systemctl status httpd

### Criar uma AMI
1. Actions 
2. Image
3. Create Image
    - Image name: nome_da_imagem

### Criar uma instância a partir de uma AMI
1. Selecionar a AMI
2. Launch

### Comandos

#### Criar uma AMI

    $ aws ec2 create-image --instance-id endereco_da_ami --name "nome_da_imagem"  --description "descricao_da_ami" --no-reboot

### Compartilhamento de uma AMI
Toda AMI está associada a uma SNAPSHOT que 
- Mudar as permissões da AMI
    1. EC2
    2. Instances
    3. Actions
    4. Modify Image Permissions

- Compartilhar a AMI de uma região para outra
    1. Selecionar a AMI
    2. Actions
    3. Copy AMI
        - Destination region

### Remover uma AMI
1. Selecionar a AMI
2. Actions
3. Deregister

### Remover o SNAPSHOT da API
1. Selecionar a SNAPSHOT
2. Actions
3. Delete

## Tags
As Tags são usadas para categorizar os recursos por meio da estrutura chave:valor

### Criar ou editar Tags
1. Tags
2. Add/Edit Tags
3. Create Tag
    1. Key
    2. Value

### EBS (Elastic Block Store)
- É um serviço de armazenamento para usar com o EC2. Em outras palavras é um disco virtual de uma instância EC2
- Tanto a EC2, quanto a sua EBS, precisam estar na mesmo zona de disponiblidade
- O volume EBS é replicado para todas as zonas de disponibilidade de uma região
- O EBS é separado da instância EC2, e por isso se uma instância pode ser removida sem perder a EBS
- Garante disponibilidade de dados, persistência de dados, criptofrafia de dados e snapshots

### SSD x HDD
- Volume baseadado em SSD: Otimizado para grandes transações de dados
- Volume basedo em HDD: Otimizado para armazenar grandes volumes de dados

### Criando um volume EBS
1. Criar uma instância
    1. Add Storage
        1. Add New Volume
        2. Volume Type
        1. Size
        2. Volume Type
        OBS: Quando o IOPS precisa ser MAIOR QUE 16,000 é recomendado o Provisioned IOPS SSD
        3. Delete on Termination

2. Criar um volume
    1. Volumes
    2. Create Volume
        1. Volume Type
        2. Size
        3. Availabity Zone
        4. Add Tag
            1. Key
            2. Value
        5. Create Volume

### Anexando um volume EBS a uma instancia EC2
1. Conectar com a maquina via SSH

        $ ssh -i MinhaChaveSSH.pem ec2-user@54.152.77.83

2. Mudar o usuario no root

        $ sudo su -

3. Listar todos os dispositivos de armazenamento

        $ fdisk -l

4. Criar um volume
    - Quando o state de um volume está como "avalaible", quer dizer que ele está disponível e preparado para ser anexado

5. Selecionar o volume

6. Actions

7. Attach Volume
    - Instance
    - Devide


### Buscar comandos associados a um determinado termo

    $ aws ec2 help | grep {termo}

### Criar um volume via terminal

    $ aws ec2 create-volume --volume-type gp2 --size 5 --availability-zone us-east-1b

### Anexar um volume via terminal

    $ aws ec2 attach-volume --volume-id vol-0ad91b69b44c62007 --instance-id i-001c3531c5a4dc46b --device /dev/sdp

### Remover um volume
1. Volumes
2. Selecionar o volume
3. Actions
4. Detach volumes
5. Actions
6. Delete volumes

## Snapshots
- É uma "foto" do estado de um volume e por isso, geralmente é um recurso usado para realizar um backup dos dados dos volumes
- Os backups sào incrementais, ou seja, é copiado apenas aquilo que mudou em relação ao snapshot mais recente

### Criar um snapshot
1. Snaphots
2. Create Snapshot
    1. Voulume ou Intance
    2. ID

Segunda maneira de criar um snapshot

1. Volume
2. Selecionar o volume
3. Actions
4. Create Snapshot
    1. Description
    2. Key
    3. Value

### Restaurar um snapshot
1. Snapshots
2. Selecionar snapshot
3. Actions
4. Create Image
5. AMI
6. Selecionar AMI
7. Launch

Segunda maneira de criar um snapshot

1. Snapshots
2. Selecionar snapshot
3. Actions
4. Create Volume
    1. Volume Type
    2. Size
    3. Availabity Zone
    4. Key
    5. Value
5. Volumes
6. Actions
7. Attach Volume
    1. Instance
    2. Device

Identficar o UUID do volumes

    $ blkid

Em sistemas operacionais Linux, náo é possível montar volumes com os mesmos UUIDs

    $ mount /dev/xdo1 /mnt

Mudar o UUID de um volume

    $ xfs_admin -U $(uuidgen) /dev/xdo1


### Lifecycle Manager
Recurso que permiter criar uma política para gerenciamento automático de snapshots

1. Volume
2. Tags
3. Add/Edit Tags    
     1. Key
     2. Value
4. Lifecycle Policy
    1. Description
    2. Select resouce type
    3. Target with these tags
    4. Lifecycle Policy Tags
    5. Policy Schedule
    6. Selecionar Copy Tags from volume
    7. Create Policy

### Security Groups
- É um firewall que controla o tráfego de entrada e saída de dados de uma instância 
- Todas as regras são permissivas, ou seja, elas estão desativadas e precisam ser ativadas, quando são necessárias
- Por padrão, os Security Groups são stateful permitem o tráfego de saída 
- É importante ser muito restritivo ao criar uma regra
- Componentes das regras
    - Protocolo: TCP, UDP, ICMP
    - Intervalo de portas: 22 (SSH) ou 2000-3000
    - Tipo de código do ICMP: echo-reply ou echo-request
    - Origem ou destino 172.29.0.3/32 ou 172.29.0.0/24

### Criar um Security Group
1. Criar uma nova instância EC2
    1. Na etapa de Configure Security Group
        1. Selecionar Create a new security group
        2. Remover a regra padrão de acesso à SSH 
        3. Clicar no botão de Review
        4. Clicar no botão de Launch
        5. Clicar no botão Launch Instances para iniciar as intancias
2. No menu Security Groups
    1. Selecionar um Security group ID
    - Inbound rules: regras de entrada e interna
    - Outbound rules: regras de saída e exerna
    - É importante evitar regrad any-to-any (regras que liberam tudo)
    2. Selecionar o Type da regra
    3. Selecionar o Source da regra (de qualquer lugar ou de um determinado ip)
    4. Clicar no botão Save rules

### PING
    $ ping [ip]

### Regras para o Security Group aceitar pacotes de Ping

1. Selecionar Custom ICMP - IPV4 em Type
2. Selecionar Echo Reply em Protocol
3. Selecionar My Ip em Source
4. Add rule
5. Selecionar Custom ICMP - IPV4 em Type
6. Selecionar Echo Request em Protocol
7. Selecionar My Ip em Source
8. Save rules

### Testar comunicação com a porta de acesso por meio do SSH
    $ telnet [ip] 22

### Regras para o Security Group aceitar o acesso via SSH
    1. Selecionar Custom ICMP - IPV4 em Type

1. Selecionar SSH em Protocol
2. Preencher o campo Port range com a porta 2222
3. Selecionar My Ip em Source
4. Add rule
5. Save rules

### Liberar a saída de Outbound rules
São as regras de saída do Security Group
1. Selecionar HTTP em Type
2. Selecionar Anywhere para Destination
3. Add rule
4. Selecionar HTTPS em Type
5. Selecionar Anywhere para Destination
6. Save rules

### Alterar um Security Group
1. Selecionar a instância
2. Clicar em Actions
3. Clicar em Networking no menu do Actions
4. Change Security Groups
    1. Selecionar o Security Group desejado para aquela instância


### Elastic IP
Adicionar um ip estático a uma instância

### Adicionar um Elastic IP a uma instância
1. Clicar em Elastic IP no submenu Network & Security
2. Clicar em Allocate Elastic IP address
    1. Selecionar Amazon's pool of IPv4 addresses
3. Selecionar o Elastic IP
3. Clicar em Actions
4. Clicar em Associate Elastic 
    1. Selecionar Instance para Resouce type
    2. Selecionar a instância em Instance
    3. Selecionar o IP privado que será associado ao Elastic IP
    4. Associate

### Chaves privadas e públicas
- O objetivo das chaves é criptotagrar e descriptografar informações de login de uma instãncia
- As chaves públicas são inseridas no arquivo authorize_keys (localizado em ~/ssh/) 
- Com as chaves privadas é possível descriptografar as informações de login a partir das chaves públicas correspondentes

### Adicionar uma chave
1. Clicar em Key Pairs no submenu Network & Security
2. Clicar em Create Key pair
    1. Colocar o nome do par de chaves no campo Name
    2. Escolher pem (SSH) em File Format
    3. Clicar em Create Key pair

### Excluir uma chave
1. Clicar em Key Pairs no submenu Network & Security
2. Selecionar a chave a ser excluida
3. Clicar no botão Actions
4. No submenu do actions, clicar em Delete

### Importar uma Key pair
- Nesse caso, o objetivo é importar uma chave já existente em outro ambiente para o ambiente da AWS
1. Criar uma chave SSH
    
        $ ssh-keygen -t rsa -b 2048 

2. Recuperar o conteúdo da chave pública
        
        $ cat id_rsa.pub

3. Clicar em Key Pairs no submenu Network & Security
4. Clicar em Actions
5. Selecionar Import Key pair do menu do Actions
    1. Preencher o nome da chave no campo Name
    2. Colar o conteúdo da chave pública no campo que está abaixo do Name 
    3. Clicar em Import Key pair

### Elastic Load Balancing (ELB)
- O ELB distribui o tráfego de entrada de aplicativos entre diversos destinos (instâncias, contêiners, endereços IP)
- É recomendado implementar o ELB quando existe mais de uma zona de dispobilidade (multi AZ)
- Quando o balanceamento de carga entre as zonas de disponibilidades está ativado, cada instância recebe a mesma quantidade de carga. Em contrapartida, quando o balanceamento de carga entre as zonas de disponibilidades está desativado, cada zona de disponibilidade recebe recebe a mesma carga e por isso pode ser que as instâncias de zonas de disponibilidades diferentes também recebam cargas diferentes, dependendo da distribuição de instâncias entre cada zona de disponibilidade
- Cada zona de disponibilidade possui uma instância responsável pelo balanceamento de carga
- Cria um ponto único de acesso (DNS) 
- Cada elastic load balancing possui hostname estático para o DNS
- Disponibiliza SSL (HTTPS)
- Um ELB pode ser privado ou público

### HTTP no ELB


- O ELB responde por meio do padrão HTTP. Basicamente, existe três tipos de códigos de retorno
    - 200: requisições realizadas com sucesso
    - 4xx: requisições realizadas com erros no lado do cliente
    - 5xx: requisições realizadas com erros no lado do servidor

### Tipos de ELB
- Existem três tipos de elastic load balancing:
    - Application Load Balancer: trabalha com os protocolos HTTP e HTTPS 
    - Network Load Balancer: trabalha com os protocolos TCP e UDP
    - Classic Load Balancer: trabalha com o HTTP, HTTPS e TCP, mas como se trata do primeiro tipo de ELB criado pela AWS, não é muito recomendado  

### Application Load Balancer
- Atua na camada de aplicação (camada 7) do modelo de referência OSI
- É recomendado para o balanceamento de tráfego HTTP e HTTPS
- Roteamento avançado 
- Escala automaticamente
- O endereço IP não é estático
- Permite o uso de stickiness (Quanto o stickness está habilitado, é possível manter uma seção de acesso com um único target. Caso o stickness estiver desabilitado, a conexão poderia estaria apontando para outros targets)

### Algoritmos de Roteamento do Application Load Balancer
- Round Robin: a requisiçào é distribuida entre os targets (uma para cada target)
- Cabeçalhos HTTP
- Path: de acordo com o path, é possível redirecionar a requisição para uma determinada pool
- Origem
- Descido

### Network Load Balancer
- Atua na camada de transporte (Camada 4) do modelo de refeência OSI
- É recomendado para o balanceamento de tráfedo TCP e UDP
- O endereço pode ser estático

### Algoritmos de Roteamento do Network Load Balancer
- Algoritmo de hash que se baseia no protocolo, endereço IP e na porta de origem, endereço IP e na porta de destino, número de sequência TCP;

### Classic Load Balancer
- Atua na camada de aplicação (camada 7) e na camada de transporte (camada 4) do modelo de referência OSI
- É praticamente legado, principalmente, quando se trata do balanceamento de tráfego HTTP e HTTPS
- Roteamento não avançado
- Endereço IP não estático
- Não é recomendado

### Gateway Load Balancer
- Com o Gateway Load Balance é possível executar, gerenciar e escalar Appliances Virtuais (Firewalls, IDS/IPS)
Exemplos: Check Point, Fortinet Paloalto, Cisco
- Atua na camada de rede (camada 3) do mode de referência OSI
- É recomendado para o balanceamento de tráfego IP
- Implementa o protocolo GENEVE na porta 6081
- Conexão entre duas ou mais redes
- Antes de uma requição chegar no seu destino (destination), ela precisa chegar no Gateway Load Balance que enviara a requição para as Appliances (responsáveis pela política de segurança) por meio do protocolo GENEVE na porta 6081
- Para o Gateway Load Balance, os Appliances são targets

### Criar um Elastic Load Balancer (Application Load Balancer)
1. Clicar em Load Balancers no submenu Load Balancing
2. Clicar em Create Load Balancer
3. Clicar em Create do Application Load Balancer
    1. Step 1: Configure Load Balancer
        1. Preencher o campo Name
        2. Selecionar a opcão HTTP do Load Balancer Protocol
        3. Selecionar a VPC
        4. Selecionar as Zonas de Disponibilidades
        4. Preenchar a Key e o seu respectivo Value em Tags
        5. Next

    2. Step 3: Configure Security Groups
        1. Selecionar um Security Group
        3. Next

    3. Step 4: Configure Routing
        1. Selecionar New target group para criar um novo Target group
        2. Preencher o campo Name
        3. Selecionar Instance para enviar todos os pacotes (tráfego) para um conjunto de instâncias
        4. Selecionar o protocolo HTTP do Target Group
        5. Preencher 80 como a porta do protocolo (a porta da instância que o Load Balancer precisa encaminhar)
        6. Selecionar o protocolo em HTTP do Health Check
        7. Colocar a pasta raiz ("/") para realizar o Health Check e determinar a integridade do serviço
        8. Configurar os parâmetros do Advanced health check settings
        9. Next
    
    4. Step 5: Register Targets
        1. Next

    5. Step 6: Review
        1. Create

4. Selecionar o Load Balancer criado nos passos anteriores
5. Clicar na aba Description
    1. Edit attributes
    2. Marcar a opção Enable do Delete Protection para evitar que o LB seja deletado acidentalmente
