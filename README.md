# Finance App - Documentos Legais

Páginas estáticas de **Política de Privacidade** e **Termos de Uso** para o Finance App.

## 🚀 Deploy na AWS

### Opção 1: S3 + CloudFront (Recomendado)

```bash
# 1. Criar bucket S3
aws s3 mb s3://finance-app-legal --region sa-east-1

# 2. Configurar bucket para hospedar site estático
aws s3 website s3://finance-app-legal --index-document index.html --error-document index.html

# 3. Upload dos arquivos
aws s3 sync . s3://finance-app-legal --exclude ".git/*" --exclude "README.md"

# 4. Configurar CloudFront (opcional, para HTTPS e CDN)
# Criar distribuição CloudFront apontando para o bucket S3
```

### Opção 2: Servir junto com Backend (Mais Simples)

Se seu backend já está rodando na AWS (EC2/ECS/EKS), basta copiar estes arquivos para a pasta `public` do seu backend:

```bash
# No diretório do backend
mkdir -p public

# Copiar arquivos
cp /caminho/para/finance-app-legal/privacy.html public/
cp /caminho/para/finance-app-legal/terms.html public/

# Configurar rota no Express (app.js ou server.js)
app.use(express.static('public'));
```

### Opção 3: Amplify (Serverless)

```bash
# 1. Instalar Amplify CLI
npm install -g @aws-amplify/cli

# 2. Inicializar projeto
amplify init

# 3. Adicionar hosting
amplify add hosting

# 4. Publicar
amplify publish
```

## 📝 URLs Esperadas

Após o deploy, estas URLs devem estar acessíveis:

- `https://finance-app.com/privacy` → `privacy.html`
- `https://finance-app.com/terms` → `terms.html`

## ✅ Verificação

Teste se as páginas estão online:

```bash
curl -I https://finance-app.com/privacy
curl -I https://finance-app.com/terms
```

## 📁 Estrutura

```
finance-app-legal/
├── index.html       # Página inicial com links
├── privacy.html     # Política de Privacidade (LGPD)
├── terms.html       # Termos de Uso
└── README.md        # Este arquivo
```

## 🔐 Atualizações

Para atualizar o conteúdo:

1. Editar os arquivos HTML
2. Fazer commit e push
3. Executar o deploy novamente

## 🛣️ Requisitos do Google Play

- [x] Política de Privacidade completa
- [x] Termos de Uso com informações de assinatura
- [x] LGPD (Lei nº 13.709/2018)
- [x] Direitos do usuário (acesso, correção, exclusão)
- [x] Contato do DPO
- [x] Regras de cancelamento e reembolso

## 📧 Contato

- **Suporte:** suporte@finance-app.com
- **DPO:** dpo@finance-app.com
