# ATIVIDADE-AWS-02

# Sobre a Atividade

1. Instalação e configuração do DOCKER ou CONTAINERD no host EC2.

. Ponto adicional para o trabalho que utiliza a instalação via script de Start Instance (user_data.sh).

2. Efectuar Deploy de uma aplicação Wordpress com:

. Recipiente de aplicação.

. Banco de dados RDS MySQL.

3. Configuração da utilização do serviço EFS AWS para estáticos do container de aplicação WordPress

4. Configuração do serviço de Load Balancer AWS para aplicação Wordpress

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


- Codigo
