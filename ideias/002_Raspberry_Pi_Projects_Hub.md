# Raspberry Pi Projects Hub

## 📋 Informações Básicas

- **Data de Criação:** 2026-07-15
- **Status:** [ ] 🟦 Rascunho | [x] 🟨 Em Análise | [ ] 🟧 Em Desenvolvimento | [ ] 🔴 Bloqueado | [ ] ✅ Concluída
- **Categorias:** pessoal, iot, web, automacao

---

## 💡 Descrição da Ideia

Um hub centralizador para hospedar e gerenciar múltiplos projetos pessoais localmente em um Raspberry Pi 5. Solução self-hosted que permite acessar todos os projetos através de uma interface unificada, sem necessidade de domínio externo ou serviço de nuvem. Todos os dados e aplicações rodando localmente na rede doméstica.

---

## 🎯 Objetivo Principal

Criar um servidor local no Raspberry Pi que funcione como ponto central para visualizar, acessar e gerenciar todos os projetos pessoais hospedados localmente, com interface intuitiva e sistema de routing/proxy para facilitar o acesso aos projetos sem precisar memorizar portas ou localhost.

---

## 🔧 Como Seria Implementado?

**Arquitetura:**
- Raspberry Pi 5 como servidor
- Sistema operacional: Raspberry Pi OS ou Ubuntu Server
- Reverse proxy: Nginx ou Traefik para rotear requisições

**Hub Principal:**
- Dashboard web mostrando todos os projetos
- Cada projeto com link, descrição, status
- Opção de iniciar/parar serviços
- Monitoramento de recursos (CPU, RAM, espaço disco)

**Routing/Masking (Opcional):**
- Reverse proxy que mapeia URLs personalizadas
- Exemplo: `projects.local`, `projeto1.local`, `projeto2.local`
- Arquivo `/etc/hosts` local para resolver domínios fictícios
- Alternativa: `http://raspberrypi.local/projeto1`, `http://raspberrypi.local/projeto2`

**Tipos de Projetos Suportados:**
- Aplicações web (Node.js, Python, etc)
- Serviços (APIs, databases)
- Dashboard/monitoramento
- Documentação
- File server

**Gerenciamento:**
- Interface para adicionar/remover projetos
- Configuração de porta, domínio virtual
- Logs de acesso e erros
- Reinicialização de serviços

---

## 📚 Referências

- Traefik: Reverse proxy moderno
- Nginx: Web server e reverse proxy
- Docker: Containerização de projetos
- Pi-hole: Similar, mas para DNS
- Homelab solutions: Proxmox, Docker Compose

---

## 💬 Notas Adicionais

Pode ser desenvolvido em fases:
1. **Fase 1:** Hub básico com Nginx + lista de projetos
2. **Fase 2:** Sistema de routing com domínios virtuais
3. **Fase 3:** Docker + Docker Compose para fácil deployment
4. **Fase 4:** Interface web avançada com gerenciamento de serviços

O RPi 5 tem poder suficiente para rodear múltiplos projetos simultaneamente. A solução é escalável e permite crescer conforme o número de projetos aumenta.

---

**Última Atualização:** 2026-07-15
