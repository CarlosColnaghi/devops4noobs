
# Cerificações AWS

## 4 tipos
- Foundational
	- É proposta para um público em geral
	- Não exige uma perspectiva muita técnica
	- Conhecer as tecnologias do serviço
		- Exemplo: Não é necessário saber os passos para subir uma EC2, mas precisa saber o que é o serviço EC2
	- Sugerido uma experiência de 6 meses em contato com o conhecimento básico sobre a cloud
- Associate
	- Sugerido uma experiência de 1 ano na implementação de soluções e solução de problemas
- Professional
	- Sugerido uma experiência de 2 anos na implementação de soluções e solução de problemas
- Specialty

## Por que tirar uma certificação?

- Validar as suas experiências
- Valoriza as suas habilidades
- Maior visibilidade no merdado de trabalho

# Criando uma conta na AWS

- Ao criar uma nova conta ela se torna elegível ao Nível Gratuito da AWS (também conhecido como Free Tier)
- O Free Tier estabele um conjunto de planos gratuítos para o uso dos recursos disponibilizados pelos serviços da AWS a partir de variáveis que dependem do serviço, do tempo de uso e consumo
- A cobertura do Free Tier corresponde à 12 meses, contudo existem serviços que são sempre gratuitos e outros que são categorizados como testes e, portanto, possuem um tempo limitado para o seu uso gratuito
- Em IAM existe um escopo para garantir a segurança da sua conta de acesso, como por exemplo, a ativação do MFA (autenciação multifator)

# AWS EC2

## O que é AWS EC2?

- Recurso computacional da Amazon representadas por máquinas chamadas de instâncias EC2

## Criando uma instância EC2

- Determinados serviços estão associados a região e por isso o console é reativo a localidade do datacenter da Amazon
	- Cada região é dividida por zonas de disponibilidade que são isoladas fisicamente (em questão de elétrica e infraestrutura) e garantem redundância e alta disponibilidade
- A AMI é a imagem de uma instância EC2 e esta associada ao software (sistema operacional)
	- O Amazon Linux, por exemplo, é uma imagem de um Red Hat compilado para a Amazon
	- Na AWS Marketplace existem uma diversidade de imagens pré-configuradas
- O tipo da instância define o shape da máquina e esta associada ao hardware (recursos computacionais)
- Uma instância EC2 está associada a um disco de armazenamento e trata-se de um serviço a parte e portanto, sobre ele, também existe uma cobrança separada da EC2
	- É importante lembrar que ao parar uma instância, os volumes dessas instâncias se mantem, e por isso ainda existe uma cobrança sobre eles
- Os Security Groups são grupos de seguranção que determinam regras de rede sobre o recurso
	- É possível descrever as regras de entrada e saída do recurso dentro da infraestrutura da Amazon, determinando o intervalo de portas, o tipo de protocolo e o ip 
	- É a partir do Security Group que torna-se possível accessar uma máquina via SSH (protocolo padrão para o gerenciamento remoto desse tipo de recurso), por exemplo
- A AWS exige a associação da instância a uma chave que permite acesso a ela por meio do SSH 

## Proteção contra exclusão

- Como o próprio nome sugere, a proteção contra exclusão imperde que uma instância seja ecerrada acidentalmente
1. Na tabela de instâncias EC2, selecione a máquina que se deseja habilitar o recurso
2. Depois de selecionar a instância, clique no botão Actions e selecione Change Termination Protection no menu Instance Settings

## Comunicação das instâncias e associação dos Security Groups às instâncias

- As máquinas são criadas em uma mesma sub-rede, contudo, para garantirem que elas se comuniquem, é necessário mudar os Security Groups
- O Security Group chamado de Default, permite todo o tráfego de entrada dentro da rede determinada em Source (rede padrão, também conhecida como Default VPC)

### Alterando a associação dos Security Group com uma EC2 Instance
1. Na tabela de instâncias EC2, selecione a máquina que se deseja mudar os Security Groups
2. Depois de selecionar a instância, clique no botão Actions e selecione Change Security Networking no menu Instance Settings
3. Selecione os Security Groups desejados para arquela instância

## Criando uma instância EC2 customizada

- O Marketplace da Amazom reúne um conjunto de imagens prontas para serem implementadas nas instâncias EC2
- Durante o lançamento de uma EC2 é possível defenir um script com comandos para serem executados assim que a máquina estiver inicializando. 
	1. Informe os comandos a serem executados no campo de texto User data na seção Advanced details
- Também é possível criar uma imagem a partir de uma instância já criada
	1. Na tabela de instâncias EC2, selecione a máquina que se deseja criar a imagem
	2. Pare a instância para evitar de criar uma imagem com serviços em execução e, portanto, evitar de criar uma máquina corrompida e garantir a integridade dos dados
	3. Clique em Actions e depois selecione a opção Create image do menu Image
	4. Preencha o nome da image

## IP dedicado (Elastic IP)

- O ip público pode mudar quando a instância é reinicida
- Para manter um ip estático, é necessário criar um Elastic IP e associar este IP à instância
	1. Entre no dashboard do Elastic IP addresses e clique em Allocate Elastic IP address
	2. Depois de criado o Elastic IP, selecine-o na tabela de Elastic IP addresses e escolha a opção Associate Elastic IP address do menu apresentado pelo botão Actions
	3. Por fim, selecione a instância que se deseja associar aquele Elastic IP
- É importante lembrar que existem cobranças sobre os IP dedicados
	- Não é cobrado enquanto este IP estiver associado a uma instância que está ligada. Contudo, o IP é cobrado se estiver reservado para instância que está desligada 
	- A cobrança também é realizada sobre os diferentes ips que estão associados a uma única instância

## Banco de dados na Amazon RDS

- A ideia é garantir que o serviço de banco de dados esteje rodando em uma instância separada da aplicação. Basicamente, a Amazon RDS é um serviço que provisiona uma instância preparado para os serviços de bancos de dados
- O RDS suporta vários tipos de bancos de dados
- Os templates Production, Dev/Test e Free tier estão diretamente relacionada com o nível ou tipo de máquina que será provisionada para o banco de dados
- É possível programar o RDS para realizar snapshots para backup do banco de dados
- A máquina não deve ser gerenciada, e sim o serviço. Ou seja, não é possível se conectar e interagir com a instância em si, mas é possivel se conectar ao banco de dados

## Infraestutura com Auto Scaling e Load Balancing

- A imagem demonstra uma infraestrutura com alta disponibilidade. Os usuários conseguem acessar os serviços por meio do navegador que enviam requisições para a rede da AWS por meio dos protocolos HTTP e HTTPS, usando, respectivamente, as postas 80 e 443. O tráfego é direcionado para um Load Balancer. O Load Balancer é responsável pela distribuição de carga e, portanto, direciona para as réplicas das instâncias onde um aplicativo está em execução. Todas as instâncias se conectam ao banco de dados para poder realizar a comunicação que garante a persistência de dados da aplicação

![[Load Balancer.png]]

## Load Balancers

- 3 tipos de Load Balancers
	- Application Load Balancer: protocolo HTTP e HTTPS
	- Network Load Balancer: outros protocolos (TCP, TLC, UDP)
1. No dashboard de Load Balancers clique em Cread Load Balancer
2. Depois, selecione o tipo Load Balancer (Application Load Balancer e Network Load Balancer)
3. Defina o scheme (Internet Facing e Internal)
	- Internet Facing: responde para a internet
	- Internal: responde somente dentro da rede da AWS
4. Defina os protolos e portas dos Listerners do Load Balancer
5. Para garantir a redundancia e, consequentemente a disponibilidade, é necessário escolher pelo menos duas Availability Zones ou subnets
6. Configure o Security Group com regras de inbound para aceitar os protocolos e as portas definidas para os Listerners
7. Configure o roteamento definindo o Target Group. O Target Group agrupa todas as instâncias que Load Balancer vai direcionar o tráfego
8. Defina o Health Check referenciando o protocolo e o caminho onde o requesição será realizada para verificar se o serviço está saudável
9. Por fim, registre  os Targets. Os Targets podem ser as instâncias ou um grupo do Auto Scaling

## Auto Scaling

- O Auto Scaling permite escalar os recursos, ou seja, criar novas instâncias de acordo o tráfego
- O Auto Scaling gerencia a quantidade de instâncias a partir do tráfego e dos parâmetros definidos pelo Auto Scaling Group
- Para configurar o Auto Scaling, primeiramente é necessário criar uma configuração de lançamento (Launch Configuration) para depois associar essa configuração ao Auto Scaling Group
	1. Clique em Create Auto Scaling Group
	2. Defina a VPC e as Subnets. É importante que as Subnets sejam as mesmas selecionadas na criação do Load Balancer
	3. Determine o tamanho do grupo (Group size), ou seja, a quantidade de instâncias
	4. Em Load Balancing, selecione a opção de receber o tráfico de um ou mais Load Balancers. Essa opção é importante para que se consiga associar a um  Auto Scaling Group.
	5. Em Target Groups, selecione o Target Group definido durante a criação do Load Balancer
	6. Defina o tipo de Health Check. Existem dois tipos: ELB e EC2. O ELB é um teste da aplicação e por isso, testa se a porta esta respondendo. Em contrapartida, o tipo EC2 considera os estados da instância (stopping, terminated). O Auto Scaling Group também usa como referência para adicionar ou remover uma instância do Target Group
- O Scaling Policy define políticas de escalonamento da quantidade de instâncias. Então, é possível definir condições baseadas em métricas, cmo consumo de processador ou memória, por exemplo

# AWS CLI

- É uma ferramenta de linha de comando integrada que permite gerenciar interagir com os recursos e serviços da AWS, assim como o console da AWS
- O acesso depende de um usuário com Access Key e Secret Key

### Descrever as informações das instâncias (Security group, regras, rede, tipos de instância, estado)

```shell
aws ec2 describe-instances
```

```shell
aws ec2 describe-instances --query "Reservations[*].Instances[*].{Instance:[InstanceId,State]}"
```

```shell
aws ec2 describe-instances --instance-id {instance_id}
```

### Parar e iniciar instâncias

```shell
aws ec2 start-instances {instance_id}
```

```shell
aws ec2 stop-instances {instance_id}
```

# Amazon Lightsail

## O que é Lightsail

- A proposta do Lightsail é tornar a nuvem mais simples (tanto em relação ao console, quanto com relação a configuração)
- Esta dentro da nuvem da Amazon e possuem suas zonas de disponibilidade
- Instâncias, snapshots para backup, balanceamento de carga, discos e entre outros
- Para criar uma instância é obrigatório realizar a definição da imagem (OS ou APP + OS) e da localidade (Região/Zona)
- Bitnami é provedor que empacota várias aplicações e distribuem elas como imagens
- É possível acessar as máquinas criadas via console ou cliente SSH

## IP Estático

- Toda vez que a instância é parada e iniciada novamente, um novo ip é criado para ela. 
	1. Vá na aba Networking e clique em Create static ip
	2. Selecione a instância
	3. Crie um nome para o ip estático
- É possível registrar o domínio em um provedor e apontar para que o Lightsail seja autoritativo do domínio por meio das zonas de disponibilidade

## SSH Client

- É possível se conectar uma instância via SSH por meio da interface do próprio navegador. Contudo, também é possível se conectar usando client e o par de chaves gerados durante a criação da instância
	1. Selecione a instância e clique em manage
	2. Clique Account page e o Lightsail vai direcionar para a aba SSH Keys
- Quando uma instância é criada, o Lightsail já cria um par de chaves. Contudo, também é possível criar um par de chaves e associar durante a instanciação
- Para cada região, o Lightsail cria automaticamente um par de chaves SSH com o nome Default

## Firewall

- São regras de rede que gerencia o tráfego de rede
	1. Clique na aba Networking de uma instância
	2. Na seção Firewall, clique em Add another e defina o tipo de protocolo e o intervalo da porta
	3. Por fim, clique em Salve para gravar as regras adicionadas
- Diferentemente do Security Group, não é possível definir o intervalo de ips que podem trafegar sobre aquela regra

## Snapshot

- Antes de criar um snapshot é importante parar a instância, porque podem existir vários arquivos que estão aberto em memória e isso pode gerar uma imagem corrompida
	1. Clique na aba Snapshots de uma instância
	2. Clique em Create snapshot
	3. A partir do snaptshots, é possível criar uma instância deste snapshot em Create new instance