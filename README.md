# Tutoriral-EFS-Teste
Esse tutorial tem o objetivo de realizar o passo a passo de criar uma instância EC2, instalr o EFS nessa instância e disponibilizar testes práticos para testar as características do serviço EFS.

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

<img src="https://github.com/user-attachments/assets/9a5242ff-0fb6-4ae2-9963-7068ed57acc5" width="800">

## Criar máquinas EC2
### Referência
<a href="https://www.youtube.com/watch?v=UIbZOjXAJ6U" target="_blank">Elástico e Totalmente Escalável: Amazon EFS</a>

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

No painel das instâncias EC2, selecione a instância que será configurada e clique em "Conectar".

<img src="https://github.com/user-attachments/assets/fc75b67e-e7c1-444a-b06b-44858cd7efb3" width="700">

Ao fim da página clique em "Conectar" novamente.

<img src="https://github.com/user-attachments/assets/fdbb95f9-9f7c-4467-b1d1-d0f93a04d795" width="500">

Agora você terá acesso ao terminal da máquina EC2.

<img src="https://github.com/user-attachments/assets/7a0a32a3-a481-498f-a1ac-a2d070cfadc9" width="500">


Execute o comando a seguir, para instalar a biblioteca de feramentas do EFS, e crie uma pasta nomeada de 'efs'. 
```
sudo yum install -y amazon-efs-utils

mkdir efs
```

Vá até a página do EFS que criamos anteriormente, clique em "Anexar" e copie o comando que conecta o sistema de arquivos usando o NFS. Com o comando, execute no terminal do EC2 para conectar com o EFS.

<img src="https://github.com/user-attachments/assets/5a681467-a7ce-4d7f-b2d2-5df954f8b10f" width="800">


Por fim, podemos ver o armazenamento do EFS conectado basta executar o comando ```df  -h```.

![image](https://github.com/user-attachments/assets/b80325e4-1834-44d4-b62b-99d6b5ef3425)

## Testar EFS
### Disponibilidade

Dentro do terminal do EC2, entre na pasta do EFS usando o comando ```cd efs```, depois crie um arquivo de texto ```sudo nano hello.txt```, e insira no arquivo um texto. Para sair do editor basta usar o comando "ctrl + x", depois digitar "y" e por fim teclar "enter".

![image](https://github.com/user-attachments/assets/445f4446-ffb9-4399-a9e1-c5a800db503d)


Agora você pode ver o arquivo executando o comando ```ls```, e usando o comando ```cat hello.txt``` pode ver o conteudo do arquivo.

![image](https://github.com/user-attachments/assets/97b3bbd1-6e01-4df8-9145-b8b369b5900c)

Agora entre na outra instância EC2, garanta que o mesmo EFS está instalado nela. E você pode entrar na pasta "efs" e rodar o comando ```cat hello.txt``` para ver o arquivo gerado na outra instância.
O caminho reverso também acontece, você pode criar um arquivo na segunda instância e acessar na primeira e todas as modificações irã replicar.

### Escalabilidade
Você pode seguir a postagem da Amazon que realiza testes de performace na criação de arquivos em EC2, usando o EFS. <a href="https://aws.amazon.com/pt/blogs/storage/how-to-test-drive-amazon-elastic-file-system/" target="_blank">How to test drive Amazon Elastic File System</a>

### Repositório de tutoriais do EFS
A amazon possui um repositório completo com tutoriais de como usar o EFS em diversas situações. <a href="https://github.com/aws-samples/amazon-efs-tutorial/" target="_blank">Amazon EFS Tutorial</a>
