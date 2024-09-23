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

<img src="https://github.com/user-attachments/assets/3ca00477-cb55-4958-8a62-8facacf99f16" width="800">


## Criar máquinas EC2
Nessa etapa vamos apenas configurar caracteristicas obrigatórias para a criação da instância EC2.
Vamos precisar de duas instâncas, então repita o processo para criar mais intâncias quando necessário.

No painel do EC2, clique no botão "Executar instância".

<img src="https://github.com/user-attachments/assets/0b7b8243-3201-495f-9a45-2984484cc12e" width="400">

Nomei a sua instância.

<img src="https://github.com/user-attachments/assets/64848a8b-4966-4f8b-aad7-6abb9361e292" width="550">

Selecione o par de chaves. Nessa etapa selecionei para prosseguir sem um par de chaves, mas sinta-se livre para selecionar outra opção.

<img src="https://github.com/user-attachments/assets/daadd075-033b-481e-a36f-29652307c2c6" width="500">

Verifique se nas configurações de Rede se está permitido o acesso através de SSH à instância.

<img src="https://github.com/user-attachments/assets/c438cfc4-cea0-4e91-9208-1612db02d63a" width="450">

E por fim, clique em "Executar instância".

<img src="https://github.com/user-attachments/assets/8480d165-e8aa-4788-9620-e3fcb57a0e52" width="300">

## Configurar EFS no EC2

## Testar EFS
### Disponibilidade
### Escalabilidade
