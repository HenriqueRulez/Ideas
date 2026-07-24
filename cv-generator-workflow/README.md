# 🎯 CV Tailored Generator Workflow

Sistema de coaching para gerar CVs customizados por vaga, com garantia de honestidade e otimização máxima.

---

## 📁 Arquivos Neste Diretório

### 1. **01_SEU_PERFIL_PROFISSIONAL.md**
Documento completo com TUDO sobre você:
- Experiências (com números e achievements)
- Skills técnicas e soft skills
- Educação
- Projetos pessoais
- Guardrails (regras que Claude deve respeitar)

**Como usar:**
- Preencha COMPLETAMENTE com informações honestas
- Seja específico (números, datas, tecnologias)
- Atualize conforme tiver novas experiências
- Use como referência para todas as conversas

**Tempo de setup:** 1-2 horas (mas reutiliza pra sempre)

---

### 2. **02_CV_COACH_PROMPT.md**
Prompt/instrução completa que você cola em nova conversa com Claude.

**Como usar:**
1. Preencha primeiro o arquivo 01_ completamente
2. Abra https://claude.ai (nova conversa)
3. Cole o conteúdo de 02_
4. Cole seu perfil preenchido do 01_
5. Pronto! Claude é seu CV Coach

---

### 3. **03_SKILL_CV_COACH.md**
Instrução detalhada de como Claude deve atuar como CV Coach.

**Como usar (Opção Avançada):**
- Salve em `.claude/skills/cv-coach.md`
- Use `/cv-coach` em futuras conversas
- Claude carrega automaticamente as instruções

---

### 4. **EXAMPLE_CV_GENERATED.md** (próximo)
Exemplo de CV gerado tailored para uma vaga.

---

## 🚀 Como Começar - Passo a Passo

### **Passo 1: Prepare Seu Perfil (30 min - 2h)**

1. Abra `01_SEU_PERFIL_PROFISSIONAL.md`
2. Preencha TUDO:
   - Experiências (com achievements!)
   - Skills (seja honesto sobre nível)
   - Educação
   - Projetos pessoais
   - Guardrails (regras para Claude)

**Dica:** Quanto mais completo, melhor os CVs gerados.

---

### **Passo 2: Crie Conversa com Claude (5 min)**

1. Vá para https://claude.ai
2. Clique em "Nova Conversa"
3. Cole `02_CV_COACH_PROMPT.md` COMPLETO
4. Aguarde Claude confirmar
5. Cole seu perfil preenchido (01_)

**Claude vai:**
- ✅ Confirmar entendeu tudo
- ✅ Validar guardrails
- ✅ Ficar pronto para gerar CVs

---

### **Passo 3: Gere CV para Vaga**

Quando achar uma vaga que gosta:

1. Copie a job description
2. Diga: "Preciso de CV tailored para essa vaga:"
3. Cole a job description
4. Claude gera CV + explicação de choices

**Resultado:**
- CV pronto para enviar
- Explicação do porquê de cada mudança
- Sugestões de melhorias reais

---

## 📋 Exemplo de Uso

### Você:
```
Preciso de CV tailored para essa vaga:

[JOB DESCRIPTION DA VAGA]
```

### Claude:
```
Analisando essa vaga...

A vaga procura: Senior Backend + 5+ anos Python...

Você tem: 6 anos Python, backend production...

Estratégia: Destacar achievements quantificáveis + skill em [tech que eles usam]

---

[AQUI VEM O CV TAILORED]

---

Explicação das choices:
- Coloquei experiência X primeiro porque é mais relevante
- Destaquei número Y porque é exatamente o que eles procuram
- Reformulei descrição Z para destacar [skill necessário]

Pontos fortes:
✅ Mostra exatamente experiência que eles procuram
✅ Backed por números reais
✅ Profissional + acessível

Gaps a trabalhar:
📚 Eles usam [tech], seria bom aprender
🏆 Tente buscar projetos com [experiência]
```

---

## 🎯 O Que Torna Isso Especial

### ✅ Honesto
- Não inventa skills
- Não exagera números
- Não mente sobre experiência

### ✅ Otimizado
- Reframes apresentação (sem mentir!)
- Usa keywords da vaga
- Destaca relevância

### ✅ Customizado
- Cada CV é tailored
- Respeita guardrails seus
- Adapta a cada vaga

### ✅ Educativo
- Explica por quê cada choice
- Aponta gaps reais
- Sugere growth genuíno

---

## 💡 Dicas de Ouro

### 1. **Preencha Bem o Perfil**
Quanto melhor/mais completo o 01_, melhor os CVs.

Inclua:
- Números (10% melhoria no performance, 2M usuarios, etc)
- Contexto (por quê foi importante)
- Aprendizados (o que ganhou)

### 2. **Use Guardrails**
Defina regras claras:
- "Nunca colocar X"
- "Sempre destacar Y"
- "Máximo Z páginas"

Claude vai respeitar SEMPRE.

### 3. **Negocie com Claude**
Se o CV gerado não ficou bom:
- "Faz parecer mais sênior"
- "Remove essa experiência"
- "Adiciona mais números"
- "Como isso seria para vaga X?"

Ele ajusta facilmente.

### 4. **Aprenda com o Feedback**
Claude aponta:
- Gaps na sua apresentação
- Skills que você deveria aprender
- Tipos de vaga que você é melhor

Use para GROWTH real.

---

## 🔄 Quando Atualizar

- **Nova experiência:** Atualize 01_
- **Novo projeto:** Atualize 01_
- **Nova skill:** Atualize 01_
- **Mudança nos guardrails:** Avise Claude na conversa

Quanto mais atualizado, melhor!

---

## 🆘 Quando Usar

### ✅ Perfeito Para:
- Encontrou vaga que gosta
- Quer CV tailored rápido
- Quer otimizar sem mentir
- Quer entender por quê do CV
- Quer feedback honesto

### ❌ Não Use Para:
- Inventar experiências (Claude vai recusar)
- Exagerar demais (vai quebrar guardrails)
- Fazer CV genérico (sempre tailored aqui)

---

## 📊 Diferença: Antes vs Depois

### ❌ CV Genérico (Risco)
```
Sou developer com X anos.
Usei Python, JavaScript e mais.
Trabalhei em várias empresas.
Tenho bachelor em CS.
```

### ✅ CV Tailored (Com Claude)
```
Senior Backend Developer com 6 anos liderando
arquitetura Python em [tech stack relevante].

Achievements:
- Redesenhou pipeline CI/CD: redução 40% em deploy time
- Liderou migração de [tech1] para [tech2]: +2M requisições/dia
- Mentored 3 junior developers → 2 promovidos a mid-level

Skills: Python, Django, PostgreSQL, [exatamente o que eles usam]
```

**Diferença:** Aumenta chance de entrevista DRASTICAMENTE.

---

## 🎉 Começando Agora

**Próximos passos:**

1. ✏️ Preencha `01_SEU_PERFIL_PROFISSIONAL.md` (1-2 horas)
2. 🌐 Abra https://claude.ai
3. 📋 Cole `02_CV_COACH_PROMPT.md` completo
4. 👤 Cole seu perfil preenchido
5. 📌 Próxima vez que achar vaga, gere CV tailored!

---

## 📝 Template de Workflow

Salve essa estrutura:

```
1. ENCONTRA VAGA
   ↓
2. COPIA JOB DESCRIPTION
   ↓
3. CONVERSA COM CV COACH (Claude)
   ↓
4. RECEBE CV TAILORED + EXPLICAÇÃO
   ↓
5. REVISA E USA COM CONFIANÇA
   ↓
6. ENVIA CANDIDATURA
```

**Tempo total:** ~10 minutos por vaga

---

**Boa sorte!** 🚀 Esse workflow aumenta chances MUITO. 💼
