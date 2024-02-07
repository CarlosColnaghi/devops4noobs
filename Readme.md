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

Esta documentação usou como referências os seguintes conteúdos:
    
- https://www.udemy.com/course/aws-na-pratica/

## Serviços

Os serviços da AWS são soluções disponibilizadas para desenvolver a infraestrutura em cloud

- EC2: ambiente de computação (máquinas)
- VPC: ambiente de rede
- Route 53: dns
- S3: armazenamento
- Cloud Watch: monitoramento de 
- IAM: gestão e controle de acessos

## AWS Free Tier

Para novos clientes, a AWS disponibiliza um nível de gratuidade chamada de Free Tier para as suas novas contas. O Free Tier possui limites dependendo do serviço e é compreendido por níveis:

    - Sempre gratuito
    - 12 meses gratuitos
    - Testes (são de curto prazo)

O Free Tier é caracterizado por não ser acumulativo, ou seja, caso não use o beneficío naquele determinado momento e com aquelas determinadas restrições ele não vai se acumular para ser usado em um próximo momento. Uma outra característica é que o Free Tier possui limites dependendo dos níveis e dos serviços

## Root User e IAM User

Existem duas maneiras de acessar o console da AWS: uma por meio de um root user e a outra a partir de um IAM user (usuário não root). O root user é usuário proprietário da conta. A partir do usuário raiz, é possível realizar as primeiras interações com o console da AWS e criar os outros usuário da conta (também chamados de IAM users). Durante o acesso ao console da AWS, enquanto o usuário root precisa inserir o e-mail da conta, o usuário IAM tem que colocar o ID da conta que esta vinculada ao root user

## Multi Factor Authentication (MFA)

É uma segunda camada de segurança representada por uma "contrasenha" dinâmica (geralmente um código de segurança):

    - MFA Virtuais: aplicativo (Authy e Google Authenticator)
    - U2F Security Key: dispositivo conectado em porta USB
    - MFA de Hardware: dispositvo que gera os códigos

Para habilitar o MFA para o root user é necessário seguir os seguintes passos:

    1. No serviço IAM, entrar na página Security Credentials
    2. Na seção Multi-factor authentication (MFA), existe o botão Assign MFA device, responsável pelo cadastro do MFA. Clique nesse botão para habilitar o MFA
    3. Por fim, é preciso selecionar o dispositivo desejado e associar um nome ao dispositivo
    4. Configurar o dispositivo de acordo com o device selecionado

Com um nome vinculado ao dispositivo, é possível cadastrar mais de um dispositivo

## Políticas de senha

As políticas de senha definem regras que precisam ser seguidas ao criar uma senha para um novo usuário

    1. No serviço IAM, basta acessar a página Account Settings
    2. Clique em editar na seção Password policy
    3. Configure as regras de acordo com duas diretrizes: IAM default ou Custom

## Contatos Alternativos

Os contatos alternativos são informações que a AWS pode usar para se comunicar com os representantes de cobrança, operação ou segurança. Em situações onde a AWS consiga identificar uma cobrança fora do padrão ou o vazamento de credenciais, ela pode tentar entrar em contato os representantes usando as informações cadastradas na conta root

## Respostas de seguraça

As respostas também são cadastradas no dashboard de configuração da conta root. O objetivo delas é criar uma outra camada de segurança e criar uma outra maneira da AWS garantir a identidade do proprietário da conta, assim como, disponibiliza um novo meio de recuperar a conta caso ela seja perdida

## AWS CLI

Existem várias manerias de interagir com AWS e a AWS CLI é uma delas. O CLI é uma aplicação integrada ao terminal que permite implementar, gerenciar e interagir com os recursos disponibilizados pela AWS. Na documentação da AWS é possível encontrar o passo a passo de instalação a partir do sistema operacional:
    
https://docs.aws.amazon.com/pt_br/cli/latest/userguide/getting-started-install.html

Atualmente, a versão recomendada para uso é a 2.x. Caso instale a versão 1.x é recomendado migrar e atualizar para a versão mais nova

### Criar um usuário para usar no AWS CLI

Usar a conta root para realizar as tarefas do dia a dia não é considerado uma boa prática. Por isso é importante criar um novo usuário e usar a conta root somente quando necessário

1. Entre no serviço de gerenciamento de acessos (IAM) e acesse a página User Groups pelo menu lateral
2. Depois, associe as políticas de acesso para esse grupo de usuários e clique no botão Create group. Nessa etapa, é possível identificar dois tipos de políticas: uma criada e gerenciada pela AWS, enquanto que a outra é criada pelos usuários
3. No menu lateral do IAM, selecione a opção para criar usuários (Users). Por fim,  preencha o nome do usuário e associe o usuário ao grupo de usuários criados anteriormente
4. Com o usuário criado, selecione-o para visualiza-lo no dashboard de gerenciamento de usuários e na aba Security credentials, clique em Create access key
5. Marque a opção Command Line Interface (CLI) para gerar as credencias de acesso e por fim, grave essas credenciais em um lugar seguro

Durante a criação de um usuário é importante saber a maneira como esse usuário quer interagir com a AWS. Se a ideia é que esse usuário acesse somente o console da AWS ou somente o CLI, é necessário marcar as respectivas caixas de seleção que esses privilégios

### Configurar as credendiais do usuário no AWS CLI

No termial execute o comando da CLI para configurar as credencias de acesso geradas durante a seção anterior:

    $ aws configure

    AWS Access Key ID: *******
    AWS Secret Access Key: *******
    Default region name: us-east-1
    Default output format: json

Para listar as credencias de acesso cadastradas no CLI é necessário rodar o seguinte comando:

    $ aws configure list

Uma credencial de acesso também pode ser cadastrada a partir de profiles. Com os perfis, o usuário consegue cadastrar mais de uma credencial de acesso:

    $ aws configure --profile my-profile

Por padrão o profile padrão é chamado de default

Para identificar o usuário da AWS que a CLI esta usando parar executar os comandos, bastar executar o seguinte comando no terminal:

    $ aws sts get-caller-identity

## Modelo de Responsabilidade Compartilhada

O modelo de responsabilidade compartilhada, como o próprio nome sugere, é representado por um conjunto de diretrizes de segurança da nuvem onde a AWS compartilha as responsabilidades com o cliente. A AWS, por exemplo, se responsabiliza do hardware e software que são entregues como serviços. Com relação ao hardware, a AWS precisa cuidar dos servidores, data centers, regiões e zonas de disponibilidade. Enquanto que, com relação ao software, a AWS se responsabiliza com a disponibilização da computação e hypervisors, armazenamento, banco de dados, rede e outros serviços SaaS (RDS e MSK, por exemplo). Em contrapartida, o cliente precisa se responsabilizar aos dados, configurações do sistema operacional e firewall e gerenciamento de acessos (IAM)

![Modelo de Responsabilidade Compartilhada](img/modelo-responsabilidade-compartilhada.png)
Fonte: https://aws.amazon.com/pt/compliance/shared-responsibility-model/

Nesse contexto, os serviços podem ser classificados como:
    
    1. on premise: o cliente possui responsabilidade sobre toda a infraestrutura do servidor
    2. iaas: a plataforma disponibiliza a infraestrutura como serviço
    3. paas: a plataforma disponibiliza a plataforma como serviço
    4. saas: a plataforma disponibiliza o software como serviço

Sobre cada serviço o compartilhamento de resposabilidades entre cliente e AWS acontece sobre aspectos diferentes:

![Modelo de Responsabilidade Compartilhada](img/modelo-responsabilidade-compartilhada-2.png)

## EC2 (Elastic Compute Cloud)

O EC2 trata-se de um serviço da AWS que disponibiliza recursos de computação com capacidade "dimensionável" onde não é necessário investimento em hardware. Esse serviço compreende os seguintes pontos:

- Instâncias (virtualização de máquinas e servidores)
- Balanceamento de carga (Load Balancer)
- Escalonamento (AWS Auto Scaling)
- Armazenamento (EBS, S3)
- Segurança (keys)

### Regiões, Zonas de Disponibilidade e Zonas Locais

Cada região é composta por pelo menos três data centers que representam as zonas de disponibilidades (também chamadas de AZ). As zonas de disponibilidades estão conectadas entre si. É muito comum encontrar o termo Multi AZ. Quando o serviço é Multi AZ, quer dizer que possui alta disponibilidade, uma vez que o serviço está hospedado em mais de uma zona de disponibilidade. Já as zonas locais se conectam a uma ou mais zonas de disponibilidade para diminuir a latência com o cliente (por estarem em locais que estão mais próximos dos clientes). As conexões entre zonas de disponibilidades, zonas locais e clientes consideram os seguintes componentes:

- Direct Connect: conexão dedicada entre uma zona local e o cliente
- Backbone: conexão entre uma zona local e uma zona de disponibilidade

### Tipos de instâncias EC2

A AWS disponibiliza vários tipos de instâncias que possuem caraceristicas próprias baseadas em seus recursos. As máquinas de uso geral, por exemplo, são caracterizadas por serem destinadas a propósitos gerais, com recursos equilibrados e intermediários. Também, determinadas famílias de máquinas são limitadas por créditos de cpu. A família T, por exemplo, (t3 e t4) é baseada nessa política. No momento em que esse limite é ultrapassado, o desempenho de processamento é reduzido ou ele se mantem, entretanto, tarifas são cobradas sobre esse limite. Basicamente, um crédito de cpu disponibiliza o desempenho de um núcleo em 100% de utilização por um minuto. As principais categorias de máquinas EC2 são para:

- Uso geral
- Otimizadas para cpu
- Otimizadas para ram
- GPU
- Otimizadas para armazenamento

Entrando no serviço de EC2 no console da AWS, no submenu ao lado, existe a opção Tipos de Instância (Instance Types). Essa opção traz uma lista com todas as instâncias disponiveis na AWS

### Modalidades de contrato

O contrato das instâncias EC2 se resumem a 3 modalidades: on-demand, reserved e spot:

- on-demand: É a modalidade padrão do contrato. Com esse contrato, o usuário paga somente pelo tempo de uso da instância, ou seja, enquanto a instância estiver desliga, não havera cobranças. Contudo, mesmo estando desligada, pode haver cobrança sobre o armazenamento, caso haja um disco associado a instância.
O pagamento é por hora ou por segundo (considerando no mínimo 60 segundos), dependendo da AMI (imagem da instância). Sobre as instâncias com Linux, por exemplo, a cobrança é realizada sobre os segundos de uso. Entretanto, já para outras instâncias (como Linux) a cobrança é realizada sobre a hora. Em outras palavras, se usar somente 30 minutos, a cobrança sera o valor da hora. A definição de preço é baseada, principalmente, na capacidade computacional. O preço também é baseado nas amis públicas e privadas. Para essa modalidade, não existe contrato a longo prazo


- reserved: Na modalidade reservada é possível economizar cerca de 72% em relação ao modelo on-demand. Com esse contrato, o usuário consegue reservar uma determinada categoria de uma instância. Nessa modalidade existem ainda 3 níveis: padrão, conversíveis e programadas. Na modalidade padrão, não é possível realizar alterações nas instâncias. Para essa modalidade o desconto é de 72%. Já a modalidade conversível permite realizar alterações nas instâncias, entretanto, o desconto é menor (54%). Por fim, as instâncias programadas são aquelas máquinas reservadas por um curto período de tempo. Com relação as formas de opção, existem 3 disponíveis: no upfront, partial e full upfront. No no upfront, não precisa pagar nada de imediato. No modelo partial upfront, é possível pagar uma parte e, por fim, o full upfront, é necessário pagar de imediato. O contrato reserved possui, no mínimo 1 ano e no máximo 3 anos. Durante a vigência do contrato não é possível cancelar, mas é possível vender as máquinas reservadas no marketplace da AWS. 

- spot: É a modalidade com o maior desconto (90% de desconto). As instâncias spots podem ser destruídas a qualquer momento, sendo que a aws envia os avisos sobre o encerramento 2 minutos antes das interrupções. Em sua contração é necessário definir o valor máximo a se pagar pela instância e a instância vai ser liberada quando tiver uma máquina disponível por esse valor. Caso o valor mude, existem 2 soluções: pagar a diferença ou deixar de usar

### Saving Plans

Também é um modelo que compreende preços menores, principalmente quando comparado com o modelo on-demand. Nesse contrato, também é necessário escolher uma categoria de instâncias, contudo, o contratante pode apenas mudar para uma categoria superior a que ele escolheu no contrato

Existem 3 categorias de saving plans: ec2, compute saving plans (compreende os serviços ec2, fargate e lambda) e sagemaker saving plans. Antes de começar a usar os saving plans, é necessário habilitar o serviço cost explorer para analisar os ambientes e começar a receber recomendações de economia. As primeiras recomendação podem começar a aparecer somente depois de 24 horas

Os preços baixos dos saving plans são respostas ao compromisso do contrato. Os termos de contrato não pode ser mudadados, entretando, é possível se inscrever planos de poupança adicionais (o que torna possível aumentar o workload do plano). O compromisso é com base no preço por hora, ou seja, o workload no mês. Portanto, é definido no contrato a carga horária de uso das instâncias. Tanto o plano compute quanto o ec2 se aplicam sobre as instâncias compreendidas pelos cluters emr, eks e ecr. Os preços dos saving plans podem ser diferentes em relação as instâncias reservadas por um contrato, quando considerado determinados sitemas operacionais (como sles, por exemplo). Os saving plans não se aplicam as máquinas contratadas por ir (reserved instances)

#### Saving plans ou on-demand?

Saving plans:

- suporta várias soluções computacionais: ec2, fargate, lambda
- são mais flexiveis, pois, permitem trocas de famílias, sistemas operacionais, tamanhos, localizações e regiões
- adaptação automática ao ambiente, porque existem recomendações a patir de cost explorer (que garantem uma automação sobre os processos de gerenciamento e monitoramento das instância)

IR:

- suporta varias soluções de banco de dados: rds, redshift e elasticsearch
- é recomendado para criar ambientes onde os aplicativos precisam estar rodando 24x7, para aproveitar o máximo do contrato
- necesita definir uma categoria específica de instância e um sistema operacional
 
### Criar instâncias EC2 (dashboard antiga)

Primeiramente, para criar as instâncias, é necessário acessar o dashboard do serviço. Depois de acessar o dashboard, siga as seguintes instruções para criar a primeira instância:

1. Selecione a opção Instances do menu lateral 

2. Clique em Launch Instance para Iniciar o processo de criação das instâncias

3. Na tela Choose an Amazon Machine Image (AMI), é necessário escolher a imagem do sistema operacional da instância (também chamado de AMI). Existem vários tipos de AMIs: AMIs criadas pelo próprio usuário, os do marketplace e os da comunidade

4. Na tela Choose an Instance Type, o usuário precisa determinar o tipo de instância (principalmente com relação aos recursos de hardware)

5. Na tela Configure Instance Details, a AWS disponibiliza a configuração da instância

6. A próxima tela (Add Storage), o usuário consegue adicionar um volume e configurar o tamanho e o tipo do disco 

7. Em Configure Security Group, o usuário consegue criar um novo grupo ou associar a instância a um grupo já criado anteriormente. O grupo de segurança determina as regras de acessar a instância

8. Em Select an existing pair or create a new key pair, crie um novo par de chaves ou selecione um par de chaves já existente. Os pares de chaves  são usados para acessar a instância via SSH

### Criar instâncias EC2 (dashboard nova)

1. Selecione a opção Instances do menu lateral 

2. Clique em Launch Instance para Iniciar o processo de criação das instância

3. Defina o nome e/ou tags da instância

4. Na seção Application and OS Images é possível escolher a imagem do sistema operacional. Em Browse more AMIs, o usuário consegue selecionar uma outra imagem que não esta presente na seção Quick Start. É recomendado usar as imagens desenvolvidades pela a AWS e/ou por seus parceiros (AWS Marketplace AMIs)

5. Observe que no lado direito, existe um pop-up com um resumo das características da máquina

6. Defina o tipo da instância

7. Defina o par de chaves para acessar a máquina via ssh

8. Na seção Network settings, é possível definir a configuração de rede. Em Advanced network configuration, o usuário consegue adicionar novos grupos de segurança e novas interfaces de rede e ips

9. Defina o tipo de armazenamento e o seu tamanho. Também é possível definir dois File systems: o efs (é um nfs que permite o compartilhamento de arquivos entre sevidores linux) e fsx (file server da microsoft)

Em EC2 Global View o usuário consegue ter uma visão global sobre todas as instâncias, vpc, secutiry group, subnet

### Comportamento de desligamento (Shutdown Behavior), Proteção de finalização (Termination Protection) e Proteçao de parada (Stop Protection)

Existem dois tipos de comportamento de desligamento: o stop e o terminate. Enquanto o objetivo do stop é parar a máquina, o terminate é finalizar (apagar). Então, quando o usuário tenta parar a máquina com o comportamento de desligamento definido como stop pelo console da AWS, a instância desliga. Caso, o comportamento de desligamento seja o de terminate, a máquina também se desliga igual ao do stop, caso esse procedimento seja executado pela console. Contudo, se entrar na máquina via terminal e tentar desligar ela, por exemplo, ela consequentemente vai se encerrar. 

A proteção de encerramento, impede que uma máquina seja finalizada acidentalmente. No console, quando usuário tenta finalizar uma instância com esse recurso habilitado, a AWS dispara um pop-up que bloqueia a operação. Contudo, esse recurso é ignorado caso o usuário tente desligar a máquina com o comportamento de desligamento configurado para terminate. A proteção de parada, assim como a proteção de finalização, tem como objetivo evitar a parada acidental de uma instância

- Shutdown behavior: comportamento executado no momento que a máquina é desligada
    - Terminate: impede que a máquina seja inicializada novamente depois de desligada (em outras palavras, a instância é terminada)
    - Stop: permite que a máquina seja inicializada novamente depois de desligada
- Termination protection: protege contra o desligamento acidental de uma máquina

### Mudar a permissão de uma chave SSH 
É importante que apenas o dono tenha a permissão de realizar a leitura da chave

    $ chmod 400 caminho_da_chave

### Conectar com uma instância EC2

    $ ssh -i caminho_da_chave nome_do_usuario@endereco_da_instancia

### Comandos

Listar todas as instâncias:
    
    $ aws ec2 describe-instances

Remover uma instância:

    $ aws ec2 terminate-instances --instance-ids "id-xyz"

Exemplo de parâmetros para criar uma instância:

    $ aws ec2 run-instances --image-id ami-0323c3dd2da7fb37d --count 1 --instance-type t2.micro --key-name chave_ssh --security-group-ids sg-0529062a5d07f7eab --subnet-id subnet-1deb2d3c

### AMI
Uma AMI é uma imagem de uma máquina. Uma instância sempre está associada à uma AMI e portanto, todas as instâncias são criadas baseadas nas AMIs. A AMI compreede todas informações necessárias para iniciar uma instância

Os tipos de AMIs definem várias características de uma instância. Por causa dessas características, por exemplo, não é possível criar uma instância em um região diferente da AMI, ao mesmo tempo que também não é possível instalar um sistema operacional diferente do que a AMI define. É possível destacar alguns tipos de AMIs:
    - Região
    - Sistema Operacional
    - Arquitetura
    - Permissões de execução (pública, explícita e implícita)
    - Armazenamento

Com relação as  permissões de execução, existem 3 permissões:
    - pública: são concedidas permissões de execução a todas as contas da AWs
    - explicita: são concedidas permissões de execução a determinadas contas da AWS
    - implicíta: são concedidas permissões de execução implícitas para uma AMI

 Por padrão, uma AMI é privada e reservada para a sua região de origem, o que torna um recurso não global. A AMI é armazenada pelo serviço do bucket s3 e portanto, a cobrança sobre a AMI é realizada a partir do custo de armazenamendo s3
 
 É possível criar uma instância com base em AMI e depois de customizar essa instância, o usuário consegue criar uma nova AMI com base na instância customizada. Uma AMI pode ser customizada em tempo de execução por meio do user-data

### Customização em tempo de execução de uma AMI
Primeiramente, é preciso iniciar o processo de criação de uma instância. O cmapo User data da seção Advanced Detail permite inserir um script que será executado durante a criação da instância. Esse campo aceita texto ou o upload de um arquivo shell com o script a ser executado.

Segue um exemplo de um script que pode ser executado em tempo de execução durante a criação da instância

    $ #!/bin/bash

    $ yum update -y
    $ yum install httpd -y
    $ systemctl start httpd
    $ systemctl enable 


### Criar uma AMI

Para criar uma AMI, primeiramente é necessário ter uma instância já criada. Depois, selecione a instância na qual se deseja criar a instância e por meio do menu de contexto Actions, selecione Image and templates e, por fim, a opção Create image. Na nova janela, preencha o nome, a descrição, o disco e as tags. Existe uma opção chamada No reboot. Quando desmarcada, a imagem será criada sem que a máquina reinicie. Gerando uma cópia da instância com essa opção desmarcada, torna o processo mais rápido e integro

### Criar uma instância a partir de uma AMI

Para criar uma instância a partir de uma AMI é recomendado entrar no dashboard das AMIs e em seguida selecionar a AMI e clicar em Launch instance from AMI

#### Comando para criar uma AMI

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
        2. Next

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

### Adicionar Targets no Elastic Load Balancer    
1. Clicar em Instances no submenu Instances do EC2
2. Clicar em Launch Instance
    1. Step 1: Choose AMI
        1. Escolher a AMI e clicar em Select
        2. Next

    2. Step 2: Choose an Instance Type
        1. Selecionar o tipo de instância (t2.micro, por exemplo)
        2. Next
    
    3. Step 3: Configure Instance Details
        1. Preencher o número de instâncias em Number of Instances (para realizar os testes com o Load Balacer, é interessante que esse número seja maior que 1)
        2. Selecionar a subnet onde o Load Balancer está localizada
        3. Em Advanced Details, na seção User Data, é possível incorporar um script para ser executado quando as instancias são criadas:

                #!/bin/bash                                                                     
                yum update -y
                yum install httpd -y
                echo "Olá, eu sou o servidor $(hostname -f)" > /var/www/html/index.html
                systemctl enable httpd && systemctl start httpd

        4. Step 4: Add Storage
            1. Next
        
        5. Step 5: Add Tags
            1. Clicar em Add Tags
            2. Preencher o campo Key e a seu respectivo Value
        
        6. Step 6: Configure Security Group
            1. Selecionar Select an existing security group
            2. Escolher um Security Group da tabela de Security Groups
            3. Clicar em Review and Launch
        
        7. Step7: Review
            1. Launch

OBSERVAÇÃO: Para realizar os testes com o serviço Apache, é importante garantir que o Security Group associado as intâncias estejam com a porta 80 e o protocolo HTTP

3. Entrar em Target Groups da Seção Load Balancing a partir do menu na lateral esquerda
4. Selecionar o Target Group desejado para adicionar os Targets
    1. Clicar em Edit da seção Attributes
        - Deregistration delay: tempo esperado antes de remover um Target de um Targer Group. O propósito é minimizar problemas de conexão enquanto o usuário estiver usando o serviço do Target.
        - Slow start duration: tempo esperado antes do Target Group permetir que um Targer comece a receber conexões.
        - Load balancing algorithm: é o algoritmo para o balanceamento de carga 
    2. Clicar na aba Targets da seção de Targets Groups
        1. Clicar em Register targets para adicionar os Targets
        2. Selecionar as instâncias que serão adicionadas como Targets
        3. Clicar em Register pending targets
5. Copiar o DNS name do Load Balancer na aba Description para poder acessar os serviços que estão rodando nas instâncias marcadas como Targets


### Health Check
É uma ferramenta para garantir a integridade dos serviços que estão rodando nas instâncias do Load Balancer. A checagem da saúde do serviço acontece periodicamente a partir do envio de requisições e checagem dos status code das respostas

1. Acessar as instâncias que estão no Target Group pelo terminal 
2. Verificar o status do serviço httpd

        $ systemctl status httpd

3. Verificar o log do serviço httpd. No log, pode ser indentificado a açào do Health Check

        $ cd /var/log/httpd
        $ tail -f access_log

### Roteamento Avançado com Elastic Load Balancer

No menu de controle dos Load Balancers, é possível criar regras que determinam os comportamentos dos tráfegos. Por padrão, toda requisição é redirecionada para um Load Balancer. Contudo, o sistema de controle da AWS permite criar novas regras. As regras podem redirionar as requisições que chegam na porta que esta rodando um serviço HTTP (porta 80), para o serviço HTTPS, por exemplo

1. Entrar no menu de controle dos Load Balancers clicando na opção 