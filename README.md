# Tutoriral-EFS-Teste
Tutorial de teste do serviço de Elastic File System da AWS.
Explicar o tutorial

### Referências

## Criar EFS

No painel do EFS, clique em "Criar"

<img src="https://github.com/user-attachments/assets/76fce2ad-8c82-4b2d-ac11-32054adcbccb" width="450">


Adicione um nome, e para esse tutorial iremos usar a VPC _default_, mas sinta-se livre para usar qualquer outra VPC.
<img src="https://github.com/user-attachments/assets/bf7586d7-5eef-4367-9238-0758ecdde2eb" width="550">


Ao entrar no sistema de arquivos, na aba de rede, é possível ver que automaticamente foi criado um acesso à todas as as subredes da nossa VPC. Isto permite que as instâncias de EC2 tenham acesso aos arquivos armazenados no EFS por toda a VPC.
<img src="https://github.com/user-attachments/assets/d1a12b21-9417-4d54-aa11-e075f0bd3581" width="1000">


Ainda na aba de rede, copie o id do grupo de segurança. Abra o painel do EC2, e acesse o recurso "Grupo de segurança".
<img src="https://github.com/user-attachments/assets/353a8851-aa69-4957-85ec-ac27850a762d" width="800">


Encontre o grupo de segurança default, você pode também usar o id que copiou na aba de rede do EFS para pesquisar o grupo.
<img src="https://github.com/user-attachments/assets/bc145d8b-ecf7-42d0-bb69-8ceb50c8d1df" width="700">

Ao entrar no grupo, clique em "Editar regras de entrada".

<img src="https://github.com/user-attachments/assets/2bffc831-8e68-4a31-87d2-c5ab6aa6ea9c" width="950">


Adicione a regra que permite que qualquer IPV4 possa acessar as máquinas usando o protocolo NFS.

<img src="https://github.com/user-attachments/assets/3ca00477-cb55-4958-8a62-8facacf99f16" width="400">


## Criar máquinas EC2

## Configurar EFS no EC2

## Testar EFS
### Disponibilidade
### Escalabilidade
