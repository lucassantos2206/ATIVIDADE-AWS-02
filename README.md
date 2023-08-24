# ATIVIDADE-AWS-02

# Sobre a Atividade

1. Instalação e configuração do DOCKER ou CONTAINERD no host EC2.

. Ponto adicional para o trabalho que utiliza a instalação via script de Start Instance (user_data.sh).

2. Efectuar Deploy de uma aplicação Wordpress com:

. Recipiente de aplicação.

. Banco de dados RDS MySQL.

3. Configuração da utilização do serviço EFS AWS para estáticos do container de aplicação WordPress

4. Configuração do serviço de Load Balancer AWS para aplicação Wordpress

5. configuração do serviço de Load
Balancer AWS para a aplicação
Wordpress
Pontos de atenção:
não utilizar ip público para saída do
serviços WP (Evitem publicar o serviço
WP via IP Público)
Trilha de Estudo Aréa/Tecnologia Assunto Descrição
sugestão para o tráfego de internet
sair pelo LB (Load Balancer Classic)

![image](https://github.com/lucassantos2206/ATIVIDADE-AWS-02/assets/139476940/b37171b3-d2c1-46ab-9726-022b2adb6b9f)


# Grupos de Segurança - Criação
Antes de iniciarmos a criação do EC2, do RDS e do EFS, recomendamos criar os Security Groups para cada um no console AWS.

O SG da EC2 deve conter as seguintes Regras de Inbound:

![image](https://github.com/lucassantos2206/ATIVIDADE-AWS-02/assets/139476940/47ddbff1-1352-48f1-a387-2194be7ac66d)

O SG do RDS deve conter a seguinte Regra de Entrada:

![image](https://github.com/lucassantos2206/ATIVIDADE-AWS-02/assets/139476940/a0a2998a-92c7-4fe1-8b66-2cc2a47ddc8b)

O SG do EFS deve conter a seguinte Regra de Entrada:

![image](https://github.com/lucassantos2206/ATIVIDADE-AWS-02/assets/139476940/7f474114-06a8-4711-ae93-f567a683d449)

# EC2 - Criando uma instância

Abra o menu de criação do EC2 no seu console AWS e vá em Launch Instance, feito isso siga os passos de criação do seu EC2 (nome, KeyPair, tipo, sistema operacional, storage) e selecione o Security Group criado para o EC2.


Esse shellscript (user_data.sh) nos auxiliará em:

+ Atualização do sistema operacional

+ Instalação do Docker e do Docker Compose

+ Configuração de configurações

+ Criação do ambiente para trabalhar com um sistema de arquivos NFS que armazenará os arquivos do WordPress

Com todos esses passos feitos, basta criar sua instância EC2.

# RDS - Criando o Amazon Relational Database Service

O RDS armazenará os arquivos do container do WordPress, então antes de partir para o acesso no EC2, recomendo criar o banco de dados primeiramente.

+ Procure pelo serviço de RDS no console AWS e vá em "Criar banco de dados"

+ Escolha o tipo de mecanismo como MySQL

+ Em "Modelos" selecione a opção "Nível Gratuito"

+ Dê um nome para sua instância RDS

+ Escolha suas credenciais do banco de dados e guarde essas informações (nome de usuário mestre e senha mestre), pois são informações necessárias para a criação do contêiner do WordPress

+ Na etapa de "Conectividade", escolha o Grupo de Segurança criado especialmente para o RDS, selecione a mesma AZ que seu EC2 criado está e em "Acesso público" escolha a opção de sim.

+ Vá em "Criar banco de dados"

+ Ao fim da criação do RDS, haverá uma etapa chamada "Configuração adicional" e nela existe um campo chamado "Nome inicial do banco de dados", esse nome também será necessário na criação do contêiner do WordPress

![image](https://github.com/lucassantos2206/ATIVIDADE-AWS-02/assets/139476940/673256a9-71d9-499f-8c1c-b16237dd0318)


# EFS - Criando o Amazon Elastic File System

+ O EFS armazenará os arquivos estáticos do WordPress. Portanto, para criá-lo corretamente e, em seguida, fazer a montagem no terminal, devemos seguir os seguintes passos:

+ Busque pelo serviço EFS ainda no console AWS e vá em “Create file system”

+ Na janela que se abre, escolha o nome do seu volume EFS

+ Na lista de "Sistemas de arquivos" clique no nome do seu EFS e vá na seção "Rede". Nessa parte vá no botão "Manage" e altere o SG para o que criamos no início especificamente para o EFS

![image](https://github.com/lucassantos2206/ATIVIDADE-AWS-02/assets/139476940/4cc26d9d-ba43-434f-b07c-5edd5ae22760)


🗝️ Acessando o EC2 e fazendo configurações

+ Para confirmar a montagem do EFS execute "df -h"

+ Para confirmar a montagem do docker execute "docker info"

# ELB - Criando o Elastic Load Balancer

Para fazer a criação do LB devemos procurar pelo serviço de Load Balancer no console AWS, clicar no botão "Create Load Balancer" e seguir os seguintes passos:

Escolha o tipo "Application Load Balancer"

![image](https://github.com/lucassantos2206/ATIVIDADE-AWS-02/assets/139476940/912e3a9d-fe6c-45d0-bb48-658588a09958)

+ Nome do load balancer

+ Escolha a VPC

+ Escolha a instancia 

+ Grupo de Segurança, escolha o que foi feito especialmente pra Load Balancer

+ Clique em Criar o Load Balancer





