# Keycloak com PostgreSQL - Docker Compose

Este projeto fornece uma configuração Docker Compose para executar o **Keycloak** (um sistema de gerenciamento de identidade e acesso) com **PostgreSQL** como banco de dados. Ideal para ambientes de desenvolvimento e testes.

## 📋 Pré-requisitos

- Docker ([Instalação](https://docs.docker.com/get-docker/))
- Docker Compose ([Instalação](https://docs.docker.com/compose/install/))
- Portas `9090` e `5432` disponíveis no host.

## 🚀 Como Executar

### 1. Clone o Repositório

```bash
git clone https://github.com/MadsonAlan/keycloak-postegres-docker.git
cd keycloak-postegres-docker
```

### 2. Configure o Arquivo .env

Crie um arquivo .env na raiz do projeto com as seguintes variáveis:

```bash
# PostgreSQL
DB_NAME=keycloak
DB_USER=keycloak
DB_PASSWORD=sua_senha_segura
DB_PORT=5432

# Keycloak Admin
KEYCLOAK_ADMIN_USER=admin
KEYCLOAK_ADMIN_PASSWORD=senha_admin
```

⚠️ Importante:

- Não commit o arquivo .env! Adicione-o ao .gitignore.

- Use senhas complexas em produção.

### 3. Inicie os Containers

```bash
docker-compose up -d
```

### 4. Acesse o Keycloak

- URL: http://localhost:9090

- Usuário Admin: admin (ou o valor de KEYCLOAK_ADMIN_USER no .env)

- Senha Admin: senha_admin (ou o valor de KEYCLOAK_ADMIN_PASSWORD no .env)

## 🔧 Configuração

Variáveis de Ambiente
|Variável| Descrição| Valor Padrão|
| -------- | ----- | ----------- |
|DB_NAME| Nome do banco de dados PostgreSQL| keycloak
|DB_USER| Usuário do PostgreSQL| keycloak
|DB_PASSWORD| Senha do PostgreSQL| Obrigatório
|KEYCLOAK_ADMIN_USER| Usuário administrador do Keycloak| admin
|KEYCLOAK_ADMIN_PASSWORD| Senha do administrador do Keycloak| Obrigatório

### Volumes

- PostgreSQL: Dados são persistidos em postgres_data.

- Keycloak: Configurações são salvas em keycloak_data (se configurado).

### Healthcheck

O PostgreSQL verifica sua prontidão a cada 10 segundos antes do Keycloak iniciar.

## 🛠️ Personalização

### Temas e Plugins

Para adicionar temas ou plugins ao Keycloak:

1. Crie um diretório themes/ ou plugins/ no projeto.

2. Monte o diretório no container no docker-compose.yml:

```yaml
volumes:
  - ./themes/:/opt/keycloak/themes/
  - ./plugins/:/opt/keycloak/providers/
```

### Rede

- Os serviços estão isolados na rede keycloak-network.

- Para expor o PostgreSQL externamente, adicione ports: - "5432:5432" (não recomendado para produção).

## 🔒 Boas Práticas de Segurança
1. Não use start-dev em produção: Remova o comando command: start-dev e configure HTTPS.

2. Atualize as credenciais padrão: Altere KEYCLOAK_ADMIN_USER e KEYCLOAK_ADMIN_PASSWORD.

3. Use HTTPS: Configure um proxy reverso (ex: Nginx) com certificados SSL.

4. Monitore os logs:

```bash
docker-compose logs -f keycloak
```
## 🚨 Solução de Problemas
### Erro de Conexão com o PostgreSQL
```bash
# Verifique se o PostgreSQL está saudável:
docker-compose logs postgres

# Teste a conexão manualmente:
docker exec -it postgres psql -U keycloak -d keycloak
```

### Portas em Uso
Altere a porta do Keycloak no docker-compose.yml:

```yaml
ports:

- "8080:8080" # Altere para uma porta livre
```
