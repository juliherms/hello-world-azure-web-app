# 🗄️ Configuração do Banco de Dados SQL Server no Azure

## 📋 Visão Geral

Este documento contém os comandos necessários para criar, configurar e gerenciar um banco de dados SQL Server no Azure para o projeto **Hello World Azure Web App**.

## ⚠️ Informações Importantes

- **Serviço Gratuito**: SQL Server no Azure é gratuito para o primeiro ano de contas Azure
- **Limite de Armazenamento**: Contas gratuitas permitem apenas 250 GB de armazenamento gratuito com bancos de dados SQL
- **Localização**: Todos os recursos serão criados na região `westus2`

## 🚀 Criação do Servidor SQL Server

### 1. Criar o Servidor SQL Server

```bash
az sql server create \
--admin-user udacityadmin \
--admin-password p@ssword1234 \
--name hello-world-server \
--resource-group resource-group-west \
--location westus2 \
--enable-public-network true \
--verbose
```

**Parâmetros:**
- `--admin-user`: Nome do usuário administrador
- `--admin-password`: Senha do administrador (⚠️ **Altere para uma senha segura!**)
- `--name`: Nome único do servidor SQL
- `--resource-group`: Grupo de recursos existente
- `--location`: Região do Azure
- `--enable-public-network`: Habilita acesso público
- `--verbose`: Mostra informações detalhadas

## 🔥 Configuração do Firewall

### 2. Permitir Acesso dos Serviços Azure

```bash
az sql server firewall-rule create \
-g resource-group-west \
-s hello-world-server \
-n azureaccess \
--start-ip-address 0.0.0.0 \
--end-ip-address 0.0.0.0 \
--verbose
```

**Explicação:** Esta regra permite que todos os serviços e recursos do Azure acessem o servidor SQL.

### 3. Permitir Acesso do Seu IP Público

```bash
az sql server firewall-rule create \
-g resource-group-west \
-s hello-world-server \
-n clientip \
--start-ip-address <SEU-IP-PÚBLICO> \
--end-ip-address <SEU-IP-PÚBLICO> \
--verbose
```

**⚠️ Importante:** Substitua `<SEU-IP-PÚBLICO>` pelo endereço IP público da sua máquina.

**Como descobrir seu IP público:**
- Acesse: [whatismyipaddress.com](https://whatismyipaddress.com/)
- Ou execute: `curl ifconfig.me` (Linux/Mac)
- Ou execute: `Invoke-RestMethod -Uri "https://api.ipify.org"` (PowerShell)

## 🗄️ Criação do Banco de Dados

### 4. Criar o Banco de Dados

```bash
az sql db create \
--name hello-world-db \
--resource-group resource-group-west \
--server hello-world-server \
--service-objective S0 \
--verbose
```

**Parâmetros:**
- `--name`: Nome do banco de dados
- `--resource-group`: Grupo de recursos
- `--server`: Nome do servidor SQL criado
- `--service-objective`: Tipo de plano (S0 = Standard, B = Basic, F = Free)
- `--verbose`: Mostra informações detalhadas

## 🗑️ Comandos de Remoção

### 5. Deletar o Banco de Dados

```bash
az sql db delete \
--name hello-world-db \
--resource-group resource-group-west \
--server hello-world-server \
--verbose
```

### 6. Deletar o Servidor SQL Server

```bash
az sql server delete \
--name hello-world-server \
--resource-group resource-group-west \
--verbose
```

**⚠️ Atenção:** Este comando irá deletar **TODOS** os bancos de dados associados ao servidor.

## 🔧 Configuração da Aplicação Flask

### String de Conexão

Após criar o banco de dados, configure a string de conexão na sua aplicação Flask:

```python
# Exemplo de string de conexão
connection_string = (
    "DRIVER={ODBC Driver 17 for SQL Server};"
    "SERVER=hello-world-server.database.windows.net;"
    "DATABASE=hello-world-db;"
    "UID=udacityadmin;"
    "PWD=p@ssword1234;"
)
```

### Variáveis de Ambiente

Configure as seguintes variáveis de ambiente:

```bash
AZURE_SQL_SERVER=hello-world-server.database.windows.net
AZURE_SQL_DATABASE=hello-world-db
AZURE_SQL_USERNAME=udacityadmin
AZURE_SQL_PASSWORD=p@ssword1234
```

## 📊 Monitoramento

### Verificar Status do Servidor

```bash
az sql server show \
--name hello-world-server \
--resource-group resource-group-west
```

### Verificar Status do Banco de Dados

```bash
az sql db show \
--name hello-world-db \
--resource-group resource-group-west \
--server hello-world-server
```

### Listar Regras de Firewall

```bash
az sql server firewall-rule list \
--server hello-world-server \
--resource-group resource-group-west
```

## 🛡️ Segurança

### Recomendações

1. **Altere a senha padrão** do administrador
2. **Use variáveis de ambiente** para credenciais
3. **Configure regras de firewall** específicas
4. **Monitore o acesso** regularmente
5. **Use sempre HTTPS** para conexões

### Limpeza de Recursos

Para remover todos os recursos relacionados ao banco de dados:

```bash
# Deletar banco de dados
az sql db delete --name hello-world-db --resource-group resource-group-west --server hello-world-server

# Deletar servidor SQL
az sql server delete --name hello-world-server --resource-group resource-group-west

# Ou deletar todo o grupo de recursos (cuidado!)
az group delete -n resource-group-west
```

## 📚 Recursos Adicionais

- [Documentação oficial Azure SQL](https://docs.microsoft.com/azure/azure-sql/)
- [Azure CLI SQL commands](https://docs.microsoft.com/cli/azure/sql)
- [Melhores práticas de segurança](https://docs.microsoft.com/azure/azure-sql/database/security-overview)

---

**⚠️ Lembre-se:** Sempre use senhas seguras e não compartilhe credenciais em repositórios públicos!
