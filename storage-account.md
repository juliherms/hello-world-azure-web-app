# 📦 Configuração da Conta de Armazenamento Azure Storage

## 📋 Visão Geral

Este documento contém as instruções para criar e configurar uma conta de armazenamento Azure Storage para o projeto **Hello World Azure Web App**. O Azure Storage é um serviço de armazenamento em nuvem que oferece armazenamento de objetos, arquivos, tabelas e filas.

## 🚀 Criação da Conta de Armazenamento

### 1. Criar a Conta de Armazenamento

```bash
az storage account create \
--name helloworld12345 \
--resource-group resource-group-west \
--location westus2
```

**Parâmetros:**
- `--name`: Nome único da conta de armazenamento (deve ser globalmente único)
- `--resource-group`: Grupo de recursos existente
- `--location`: Região do Azure onde a conta será criada

**⚠️ Importante:** 
- O nome da conta de armazenamento deve ser **globalmente único** em todo o Azure
- A conta será criada como **General-Purpose V2** por padrão
- A **camada de acesso** será definida como **Hot** por padrão (não pode ser alterada durante a criação)

## 📁 Criação do Contêiner

### 2. Criar o Contêiner de Imagens

```bash
az storage container create \
--account-name helloworld12345 \
--name images \
--auth-mode login \
--public-access container
```

**Parâmetros:**
- `--account-name`: Nome da conta de armazenamento criada
- `--name`: Nome do contêiner (pasta virtual)
- `--auth-mode login`: Usa autenticação do Azure CLI
- `--public-access container`: Permite acesso público de leitura aos blobs

**Níveis de Acesso Público:**
- `container`: Acesso público de leitura para contêiner e blobs
- `blob`: Acesso público de leitura apenas para blobs
- `off`: Sem acesso público (padrão)

## 🔍 Verificação no Portal Azure

Após executar os comandos, você pode verificar se a conta de armazenamento e o contêiner foram criados com sucesso:

1. **Acesse o [Portal Azure](https://portal.azure.com)**
2. **Navegue para "Contas de armazenamento"**
3. **Procure pela conta `helloworld12345`**
4. **Clique na conta e vá para "Contêineres"**
5. **Verifique se o contêiner `images` foi criado**

## 📊 Comandos de Verificação via CLI

### Verificar Status da Conta de Armazenamento

```bash
az storage account show \
--name helloworld12345 \
--resource-group resource-group-west
```

### Listar Contêineres

```bash
az storage container list \
--account-name helloworld12345 \
--auth-mode login
```

### Verificar Propriedades do Contêiner

```bash
az storage container show \
--account-name helloworld12345 \
--name images \
--auth-mode login
```

## 🔧 Configuração da Aplicação Flask

### String de Conexão

Após criar a conta de armazenamento, configure a string de conexão na sua aplicação Flask:

```python
# Exemplo de configuração para Azure Storage
from azure.storage.blob import BlobServiceClient

# String de conexão
connection_string = "DefaultEndpointsProtocol=https;AccountName=helloworld12345;AccountKey=<SUA-CHAVE>;EndpointSuffix=core.windows.net"

# Ou use variáveis de ambiente
account_name = "helloworld12345"
account_key = "<SUA-CHAVE>"

# Criar cliente do serviço
blob_service_client = BlobServiceClient.from_connection_string(connection_string)
```

### Variáveis de Ambiente

Configure as seguintes variáveis de ambiente:

```bash
AZURE_STORAGE_ACCOUNT=helloworld12345
AZURE_STORAGE_KEY=<SUA-CHAVE>
AZURE_STORAGE_CONNECTION_STRING="DefaultEndpointsProtocol=https;AccountName=helloworld12345;AccountKey=<SUA-CHAVE>;EndpointSuffix=core.windows.net"
```

### Obter Chave de Acesso

Para obter a chave de acesso da conta de armazenamento:

```bash
az storage account keys list \
--account-name helloworld12345 \
--resource-group resource-group-west
```

## 📤 Upload de Arquivos

### Upload de Imagem via CLI

```bash
az storage blob upload \
--account-name helloworld12345 \
--container-name images \
--name exemplo.jpg \
--file caminho/para/imagem.jpg \
--auth-mode login
```

### Upload de Múltiplos Arquivos

```bash
az storage blob upload-batch \
--account-name helloworld12345 \
--source caminho/para/pasta \
--destination images \
--auth-mode login
```

## 🗑️ Comandos de Remoção

### Deletar Contêiner

```bash
az storage container delete \
--account-name helloworld12345 \
--name images \
--auth-mode login
```

### Deletar Conta de Armazenamento

```bash
az storage account delete \
--name helloworld12345 \
--resource-group resource-group-west
```

**⚠️ Atenção:** Este comando irá deletar **TODOS** os dados armazenados na conta.

## 🛡️ Segurança e Boas Práticas

### Recomendações

1. **Use variáveis de ambiente** para credenciais
2. **Configure regras de rede** para restringir acesso
3. **Use SAS tokens** para acesso temporário
4. **Monitore o uso** da conta regularmente
5. **Configure backup** para dados importantes

### Configurar Regras de Rede

```bash
# Permitir apenas IPs específicos
az storage account network-rule add \
--resource-group resource-group-west \
--account-name helloworld12345 \
--ip-address <SEU-IP-PÚBLICO>

# Permitir acesso de redes virtuais
az storage account network-rule add \
--resource-group resource-group-west \
--account-name helloworld12345 \
--subnet <SUBNET-ID>
```

## 📊 Monitoramento

### Verificar Uso da Conta

```bash
az storage account show \
--name helloworld12345 \
--resource-group resource-group-west \
--query "usageInBytes"
```

### Listar Blobs no Contêiner

```bash
az storage blob list \
--account-name helloworld12345 \
--container-name images \
--auth-mode login
```

## 📚 Recursos Adicionais

- [Documentação oficial Azure Storage](https://docs.microsoft.com/azure/storage/)
- [Azure CLI Storage commands](https://docs.microsoft.com/cli/azure/storage)
- [Melhores práticas de segurança](https://docs.microsoft.com/azure/storage/common/storage-security-guide)
- [SDK Python para Azure Storage](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-python)

---

**⚠️ Lembre-se:** 
- O nome da conta de armazenamento deve ser globalmente único
- Configure sempre as variáveis de ambiente para credenciais
- Monitore o uso para evitar custos inesperados
- Use regras de rede para restringir acesso quando possível
