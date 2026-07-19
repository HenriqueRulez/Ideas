# Marketplace Auto Buyer - Scraper & Notificações

## 📋 Informações Básicas

- **Data de Criação:** 2026-07-15
- **Status:** [ ] 🟦 Rascunho | [x] 🟨 Em Análise | [ ] 🟧 Em Desenvolvimento | [ ] 🔴 Bloqueado | [ ] ✅ Concluída
- **Categorias:** web, automacao, startup

---

## 💡 Descrição da Ideia

Web scraper inteligente que monitora automaticamente Facebook Marketplace e OLX Portugal em busca de produtos específicos. Notifica o usuário em tempo real quando novos itens correspondentes aos critérios de busca aparecem. No cenário avançado, a aplicação tentaria automatizar o processo de compra, completando formulários e enviando requisições de compra com segurança.

---

## 🎯 Objetivo Principal

Criar uma ferramenta que automatize a busca por produtos desejados em marketplaces, notificando o usuário instantaneamente e opcionalmente executando ações de compra automática, economizando tempo e aumentando as chances de adquirir itens procurados antes de outros compradores.

---

## 🔧 Como Seria Implementado?

**Arquitetura:**
- Backend: Node.js/Python com Puppeteer ou Selenium para scraping
- Banco de dados: MongoDB/PostgreSQL para armazenar listings
- Fila de tarefas: Bull/Celery para processar scrapes periodicamente
- Notificações: Webhook, email, push notification, webhook Discord/Telegram

**Web Scraping:**
- Facebook Marketplace:
  - Usar Puppeteer/Playwright para navegar (requer controle de browser)
  - Autenticação com credenciais do usuário
  - Extração de título, preço, imagens, localização, descrição
  
- OLX Portugal:
  - Scraping de HTML ou API (se disponível)
  - Extração de dados dos anúncios
  - Rastreamento de novos posts

**Filtros e Alertas:**
- Criar watchlists com critérios:
  - Palavras-chave
  - Faixa de preço
  - Localização/região
  - Condição do produto
  - Tipo de vendedor
  
- Sistema de notificações:
  - Email
  - SMS
  - Push notification
  - Webhook para Discord/Telegram
  - Webhook customizado

**Compra Automática (Desafio Técnico):**
- Segurança: Criptografar credenciais do usuário
- Facebook Marketplace:
  - Automatizar clique em "Enviar Mensagem" ou "Comprar"
  - Preencher formulários de pagamento
  - Validação de captcha (desafio)
  
- OLX:
  - Enviar mensagens automáticas
  - Submeter ofertas de compra
  - Integração com métodos de pagamento

**Funcionalidades Core:**
- ✅ Criar watchlists com filtros customizados
- ✅ Scraping automático periódico
- ✅ Detecção de novos itens
- ✅ Notificações em tempo real
- ✅ Dashboard com histórico de itens
- ✅ Sistema de alertas configurável
- ✅ Gestão de preferências
- ✅ Relatórios de atividades
- ✅ Contato automático com vendedores (mensagens)
- ✅ Tentativa de compra automática (opcional/avançado)

---

## 📚 Referências

- Puppeteer: Browser automation
- Selenium: Web testing/scraping
- Playwright: Cross-browser automation
- Bull/BullMQ: Job queue para Node.js
- Celery: Job queue para Python
- Telegram/Discord APIs: Notificações
- Facebook Login API: Autenticação

---

## 💬 Notas Adicionais

**Desafios Técnicos:**
1. Facebook Marketplace frequentemente detecta e bloqueia bots
2. OLX pode ter proteção contra scraping
3. Captchas são obstáculo para automação de compra
4. Autenticação e segurança de credenciais é crítica
5. Legal: Verificar termos de serviço (ToS) dos marketplaces

**Fases de Desenvolvimento:**
1. **MVP:** Scraper simples + notificações básicas
2. **V2:** Filtros avançados + múltiplas fontes
3. **V3:** Dashboard web
4. **V4:** Tentativa de envio automático de mensagens
5. **V5:** Integração de pagamento e compra automática

**Alternativas:**
- Usar APIs oficiais se disponíveis (menos scraping)
- Proxy/VPN para evitar bloqueios
- Detecção de captcha com OCR ou serviço externo

**Monetização Potencial:**
- Freemium (5 watchlists grátis, premium ilimitado)
- Assinatura mensal
- Comissão em vendas realizadas

---

**Última Atualização:** 2026-07-15
