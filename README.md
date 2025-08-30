# Hello World Azure Web App

## 📋 Descrição

Este é um projeto de aplicação web desenvolvido em **Python** utilizando o framework **Flask**, projetado para ser implantado no **Azure App Service**. É uma aplicação web básica que serve como template ou ponto de partida para projetos mais complexos.

## 🚀 Funcionalidades

- **Página Inicial**: Apresentação da aplicação
- **Página Sobre**: Informações sobre o projeto
- **Página de Contato**: Formulário de contato
- **Interface Responsiva**: Design adaptável usando Bootstrap
- **Navegação Intuitiva**: Menu de navegação com todas as páginas

## 🏗️ Arquitetura do Projeto

```
hello-world-azure-web-app/
├── application.py              # Arquivo principal de execução
├── FlaskTemplate/             # Pacote principal da aplicação
│   ├── __init__.py           # Inicialização da aplicação Flask
│   ├── views.py              # Rotas e controladores
│   ├── templates/            # Templates HTML
│   │   ├── layout.html       # Layout base da aplicação
│   │   ├── index.html        # Página inicial
│   │   ├── about.html        # Página sobre
│   │   └── contact.html      # Página de contato
│   └── static/               # Arquivos estáticos
│       ├── content/          # CSS e estilos
│       ├── scripts/          # JavaScript
│       └── fonts/            # Fontes
├── requirements.txt           # Dependências Python
└── README.md                 # Este arquivo
```

## 🛠️ Tecnologias Utilizadas

- **Backend**: Python 3.x
- **Framework Web**: Flask 3.0.2
- **Frontend**: HTML5, CSS3, JavaScript
- **Framework CSS**: Bootstrap 3.x
- **Templates**: Jinja2
- **Banco de Dados**: SQLAlchemy (configurado para Azure)
- **Armazenamento**: Azure Storage Blob
- **Formulários**: WTForms

## 📦 Dependências

As principais dependências incluem:

- `Flask==3.0.2` - Framework web
- `Flask-SQLAlchemy==3.1.1` - ORM para banco de dados
- `Flask-WTF==1.2.1` - Integração com WTForms
- `azure-storage-blob==12.19.0` - Cliente Azure Storage
- `pyodbc==5.1.0` - Driver ODBC para SQL Server
- `Werkzeug==3.0.1` - Utilitários WSGI

## 🚀 Como Executar Localmente

### Pré-requisitos

- Python 3.7 ou superior
- pip (gerenciador de pacotes Python)

### Passos para Execução

1. **Clone o repositório**
   ```bash
   git clone <url-do-repositorio>
   cd hello-world-azure-web-app
   ```

2. **Crie um ambiente virtual**
   ```bash
   python -m venv .venv
   ```

3. **Ative o ambiente virtual**
   - **Windows**:
     ```bash
     .venv\Scripts\activate
     ```
   - **Linux/Mac**:
     ```bash
     source .venv/bin/activate
     ```

4. **Instale as dependências**
   ```bash
   pip install -r requirements.txt
   ```

5. **Execute a aplicação**
   ```bash
   python application.py
   ```

6. **Acesse no navegador**
   ```
   http://localhost:3000
   ```

## 🌐 Rotas da Aplicação

- **`/` ou `/home`**: Página inicial
- **`/about`**: Página sobre o projeto
- **`/contact`**: Página de contato

## ☁️ Implantação no Azure

Este projeto está configurado para ser implantado no **Azure App Service**. Para implantar:

### Pré-requisitos

- **Azure CLI** instalado no seu computador
- **Conta Azure** ativa

### Passos para Deploy

1. **Faça login no Azure**
   ```bash
   az login
   ```
   Este comando abrirá uma janela do navegador para autenticação.

2. **Crie o App Service**
   ```bash
   az webapp up --resource-group resource-group-west --name hello-world1234 --sku F1 --verbose
   ```
   
   **Parâmetros do comando:**
   - `--resource-group`: Nome do grupo de recursos (crie um se não existir)
   - `--name`: Nome único para sua aplicação web
   - `--sku`: Plano de preços (F1 = Free, B1 = Basic, S1 = Standard)
   - `--verbose`: Mostra informações detalhadas durante o deploy

3. **Configure as variáveis de ambiente** no Azure:
   - `SERVER_HOST`: Host do servidor
   - `SERVER_PORT`: Porta do servidor

4. **Configure o banco de dados** Azure SQL se necessário

### 🗑️ Como Deletar a Aplicação

Para remover completamente a aplicação e todos os recursos associados:

```bash
az group delete -n resource-group-west
```

**⚠️ Atenção:** Este comando irá deletar **TODOS** os recursos dentro do grupo de recursos, incluindo:
- App Service
- Plano de hospedagem
- Banco de dados (se configurado)
- Storage accounts
- Outros recursos Azure

**Alternativa mais segura:** Se quiser deletar apenas o App Service específico:
```bash
az webapp delete --name hello-world1234 --resource-group resource-group-west
```

## 🔧 Configuração

### Variáveis de Ambiente

- `SERVER_HOST`: Host do servidor (padrão: localhost)
- `SERVER_PORT`: Porta do servidor (padrão: 3000)

### Banco de Dados

O projeto está configurado para usar SQLAlchemy com Azure SQL Database. Configure as variáveis de conexão conforme necessário.

## 📁 Estrutura dos Templates

- **`layout.html`**: Template base com navegação e estrutura comum
- **`index.html`**: Página inicial da aplicação
- **`about.html`**: Página com informações sobre o projeto
- **`contact.html`**: Página de contato

## 🎨 Estilos e JavaScript

- **Bootstrap 3.x**: Framework CSS responsivo
- **jQuery**: Biblioteca JavaScript
- **Modernizr**: Detecção de recursos do navegador
- **CSS personalizado**: Arquivo `site.css` para estilos específicos

## 🤝 Contribuição

Para contribuir com este projeto:

1. Faça um fork do repositório
2. Crie uma branch para sua feature (`git checkout -b feature/nova-feature`)
3. Commit suas mudanças (`git commit -am 'Adiciona nova feature'`)
4. Push para a branch (`git push origin feature/nova-feature`)
5. Crie um Pull Request

## 📝 Licença

Este projeto está sob a licença MIT. Veja o arquivo LICENSE para mais detalhes.

## 📞 Suporte

Para dúvidas ou suporte:
- Abra uma issue no repositório
- Entre em contato através da página de contato da aplicação

## 🔄 Histórico de Versões

- **v1.0.0**: Versão inicial com funcionalidades básicas
- Suporte a Flask 3.x
- Integração com Azure
- Interface responsiva com Bootstrap

---

**Desenvolvido com ❤️ para Azure App Service**
