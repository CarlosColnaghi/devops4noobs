
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

## Infraestutura de alta disponibilidade com o Auto Scaling

- A imagem demonstra ua infraestrutura com alta disponibilidade. Os usuários conseguem acessar os serviços por meio do navegador que enviar requisições para a rede da AWS por meio dos protocolos HTTP e HTTPS, usando, respectivamente, as postas 80 e 443. O tráfego é direcionado para um Load Balancer. O Load Balancer é responsável pela distribuição de carga e, portanto, direciona as réplicas das instâncias onde um aplicativo está em execução. Todas as instâncias se conectam ao banco de dados para poder realizar a comunicação que garante a persistência de dados

![[Load Balancer.png]]

- 3 tipos de Load Balancers
	- Application Load Balancer: protocolo HTTP e HTTPS
	- Network Load Balancer: outros protocolos (TCP, TLC, UDP)