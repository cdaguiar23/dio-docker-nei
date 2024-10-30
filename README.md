Este repositório contém um ambiente Docker configurado para uma aplicação web em PHP com servidor MySQL e PhpMyAdmin para gerenciamento do banco de dados. O projeto foi criado como parte do curso oferecido pela DIO (Digital Innovation One).

## Configuração do Projeto

O projeto utiliza três serviços principais definidos no arquivo `docker-compose.yml`:

- **Web**: Container com PHP e Apache.
- **DB**: Container com MySQL 5.7.
- **PhpMyAdmin**: Container para gerenciamento do banco de dados MySQL.

### Estrutura do `docker-compose.yml`

- **Versão**: `3.11`
- **Rede**: Todos os serviços estão conectados à mesma rede `minha-rede`, com driver `bridge`.

### Serviços

1. **Web (PHP e Apache)**
   - **Imagem**: `webdevops/php-apache:alpine-php7`
   - **Portas**: Mapeamento da porta `4500` para a porta `80` do container.
   - **Volumes**: Sincroniza o diretório local `/data/php/` com `/app` no container.

2. **DB (MySQL)**
   - **Imagem**: `mysql:5.7`
   - **Variáveis de Ambiente**:
     - `MYSQL_ROOT_PASSWORD`: Senha do usuário root do MySQL.
     - `MYSQL_DATABASE`: Nome do banco de dados a ser criado no início (`testedb`).
   - **Portas**: Porta `3307` no host mapeada para a porta `3306` do container MySQL.
   - **Volumes**: Sincroniza o diretório local `/data/mysql-C` com `/var/lib/mysql` no container.

3. **PhpMyAdmin**
   - **Imagem**: `phpmyadmin/phpmyadmin`
   - **Variáveis de Ambiente**:
     - `MYSQL_ROOT_PASSWORD`: Senha do usuário root para conexão com o MySQL.
   - **Portas**: Porta `8082` no host mapeada para a porta `80` do container PhpMyAdmin.
   - **Volumes**: Configurações adicionais podem ser especificadas em `/data/php/admin/uploads.ini`.

## Como Usar

Para iniciar os containers, execute o seguinte comando na pasta raiz do projeto:


`docker-compose up -d`






### Acessando os Serviços

Os serviços estarão acessíveis através das seguintes URLs:

- **Aplicação Web (PHP)**: [http://localhost:4500](http://localhost:4500)
- **PhpMyAdmin**: [http://localhost:8082](http://localhost:8082)

### Notas

- Certifique-se de que os diretórios `/data/php/` e `/data/mysql-C` existam e estejam corretamente configurados em seu sistema antes de iniciar os containers.
- Para parar os containers, utilize o comando:


  `docker-compose down`
