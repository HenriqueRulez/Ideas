# Memory Match Solver — Assistente e Autoplayer para o Minigame do IdleOn

## 📋 Informações Básicas

- **Data de Criação:** 2026-07-15
- **Status:** [ ] 🟦 Rascunho | [x] 🟨 Em Análise | [ ] 🟧 Em Desenvolvimento | [ ] 🔴 Bloqueado | [ ] ✅ Concluída
- **Categorias:** pessoal, automacao, games, computer-vision, python

---

## 💡 Descrição da Ideia

Aplicação Python desktop que resolve o minigame **Memory Match** do IdleOn (versão desktop). A aplicação captura a janela do jogo, detecta o tabuleiro, identifica as cartas por assinatura visual e mantém memória perfeita do que já foi revelado.

Opera em dois modos:

- **Modo Assistente:** overlay transparente por cima do jogo (com o jogo clicável por trás) marcando cada carta já identificada com um número. Números iguais = par. O utilizador joga normalmente, com memória perfeita à vista.
- **Modo Automático:** a aplicação executa os cliques sozinha, seguindo a política ótima, priorizando eficiência (menos tentativas e menos tempo).

O alvo é **um único jogo, específico e conhecido**. Não há intenção de generalizar para outros jogos da memória.

---

## 🎯 Objetivo Principal

Limpar o máximo de fases possível do Memory Match sem perder por tempo esgotado ou tentativas esgotadas, explorando o facto de o jogo depender exclusivamente de memória — uma capacidade em que o software é perfeito e o humano não.

---

## 🎮 Mecânicas do Jogo (levantadas)

Base factual sobre a qual o resto do documento assenta:

| Mecânica | Comportamento |
|---|---|
| Estado inicial | Todas as cartas escondidas (fundo verde liso). Nenhuma revelação inicial. |
| Emparelhamento | Toda carta tem **exatamente um** gémeo. Nunca 3+ iguais. |
| Objetivo da fase | Limpar o tabuleiro inteiro → avança para a fase seguinte. |
| Tabuleiro | Cresce a cada fase. **Não é um retângulo perfeito** — tem células vazias no meio da malha. |
| Bónus de linha | No **2.º clique do round** (e só uma vez por round), a **linha inteira da 2.ª carta** é revelada. Volta a esconder-se após ~2s. |
| Erro | O par errado volta a esconder-se ~2s após o 2.º clique. |
| Tempo | Barra decrescente, reinicia a cada round. Tempo esgotado = **game over**. |
| Tentativas | Contador limitado. Tentativas esgotadas = **game over**. |
| Âncora de round | Texto `Memory Match round #N` no canto superior esquerdo. |
| Âncora de tentativas | Contador uma linha abaixo do identificador de round. |
| Modo treino | Existe. Útil para calibrar sem risco de perder progresso real. |

---

## 🧠 Estratégia — o núcleo do projeto

Esta é a parte com valor real. O reconhecimento visual é problema resolvido; a decisão não é.

### O bónus de linha é um recurso de uso único

Como o bónus só dispara no 2.º clique do round, ele não é uma consequência — é uma **decisão**. A aplicação escolhe onde gastá-lo, e a escolha correta é sempre a mesma:

1. **1.º clique:** qualquer carta **fora** da linha alvo. (Se fosse dentro, essa carta seria revelada de graça pelo bónus e o clique não teria comprado informação nenhuma.)
2. **2.º clique:** carta na linha com **mais células ocupadas**.

Resultado: `tamanho_da_maior_linha + 1` cartas identificadas ao custo de 1 tentativa. Numa fase avançada isso pode ser um terço do tabuleiro logo à primeira jogada.

Corolário operacional: **o frame do bónus é o frame mais denso em informação de todo o round.** Perdê-lo custa uma linha inteira e é irrecuperável. É ele que dita o requisito de taxa de captura.

### Política para o resto do round

Memória perfeita transforma o resto num problema simples. A política:

```
enquanto existirem cartas DESCONHECIDAS:
    clique 1 → uma carta DESCONHECIDA X
    se o desenho de X corresponde a uma carta CONHECIDA e por limpar Y:
        clique 2 → Y                      (limpa um par E ganha informação)
    senão:
        clique 2 → outra carta DESCONHECIDA Z   (ganha 2 cartas de informação)

quando não restarem DESCONHECIDAS:
    limpar os pares conhecidos em banco, 1 tentativa cada
```

**Porquê não limpar os pares conhecidos assim que aparecem:** um par conhecido não expira — a memória é da aplicação, não do ecrã. Limpá-lo cedo gasta uma tentativa que rende **zero** informação nova. Enquanto houver cartas desconhecidas, toda tentativa deve identificar pelo menos uma carta nova. Os pares ficam "em banco" e são descontados no fim, a 1 tentativa cada — custo que seria pago de qualquer maneira. Esta ordenação domina estritamente a alternativa de limpar à medida que se descobre.

### Consciência do relógio

A barra de tempo é lida como barra de progresso (largura em píxeis), sem OCR. Serve para decidir se ainda há margem para uma tentativa exploratória antes do reset do round. Como o tempo esgotado é game over, o relógio é restrição dura e o modo automático deve clicar tão rápido quanto o jogo aceitar.

---

## 🔧 Como Seria Implementado?

### Captura

Capturar **a janela do IdleOn** (`PrintWindow` / Windows Graphics Capture), **não o ecrã inteiro**.

Isto não é detalhe de performance — é correção. Capturar o ecrã capturaria o próprio overlay desenhado por cima das cartas, criando realimentação: a aplicação leria os seus próprios números como se fossem parte do jogo. Como reforço, aplicar `SetWindowDisplayAffinity(WDA_EXCLUDEFROMCAPTURE)` à janela do overlay.

Taxa alvo: **~15 fps**, restrita à região do tabuleiro. A janela de ~2s do bónus e do flip-back é o prazo a cumprir.

### Deteção do tabuleiro

O fundo verde liso das cartas escondidas é uma prenda — dispensa qualquer deteção sofisticada:

1. Máscara HSV sobre o verde → contornos → um blob por carta escondida.
2. Centroides agrupados em Y dão as linhas; em X dão as colunas.
3. O passo da malha sai da distância entre centroides adjacentes.
4. Projeta-se a malha sobre a bounding box do tabuleiro e testa-se cada posição: verde = escondida, arte = revelada, fundo do jogo = **célula vazia**.

Consequências: as células vazias caem fora sozinhas, o formato irregular deixa de ser problema, e o tabuleiro a crescer a cada fase é redetetado por frame sem recalibração manual.

### Identificação das cartas

**Perceptual hash (dHash 9x8 → 64 bits)** do interior da célula, comparação por distância de Hamming (limiar ~5).

Sem ML, sem OCR, sem template matching, sem dataset, sem treino. Arte pixel art com render estável colapsa a um inteiro de 64 bits, e cartas iguais dão distância ≈ 0.

Dois cuidados:
- **Inset na recorte** da célula, para excluir borda e artefactos da rotação de virar.
- **Só ler uma célula quando estável**: hash idêntico em 2 frames consecutivos. Isto rejeita frames apanhados a meio da animação de rotação.

**O catálogo pré-mapeado não é fundacional.** Dentro de um round só é preciso comparar cartas **entre si** — hash contra hash. Um catálogo persistente (construído no modo treino) só passa a ser necessário se a arte renderizar com variação entre instâncias. Arranca-se sem ele; entra apenas se a comparação direta falhar.

### Máquina de estados

- **Mudança de round:** recorta-se a faixa do `Memory Match round #N` e tira-se o hash dela. Hash mudou → round novo → limpa memória e rearma o bónus de linha. Detetar *mudança* chega; não é preciso ler o número. Elimina Tesseract por completo.
- **Tentativas restantes:** faixa uma linha abaixo, mesma técnica. Em modo automático o contador também é mantido internamente e o ecrã serve de validação cruzada.
- **Game over:** desaparecimento das âncoras ou barra de tempo a zero → para tudo.

### Overlay

- PySide6, frameless, always-on-top, fundo translúcido.
- **Click-through** via `WS_EX_TRANSPARENT | WS_EX_LAYERED` (`SetWindowLong`, pywin32) — o jogo continua clicável por trás, que é requisito.
- Desenha um número pequeno em cada carta já identificada. Números iguais = par. Mínimo e legível, sem poluir.
- Segue a posição da janela do jogo (poll do rect).

### Modo automático

- Cliques por `SendInput` (pydirectinput), com coordenadas do centroide da célula convertidas de cliente para ecrã.
- Sem humanização de timings: o objetivo declarado é eficiência.
- Delay entre cliques configurável, calibrado ao bloqueio de input do jogo.

### Interface de controlo

Janela simples e separada: Start / Stop, seletor de modo (Assistente ↔ Automático), hotkey global de paragem, e ajustes (limiares HSV e de hash, delay de clique, opacidade do overlay, taxa de captura).

### Módulos

```
capture.py    captura da janela
board.py      deteção da malha e das células
identify.py   dHash e memória do round
state.py      âncoras de round/tentativas, máquina de estados
solver.py     política de decisão
overlay.py    HUD click-through
input.py      cliques
app.py        interface de controlo e configuração
```

### Dependências

`opencv-python`, `numpy`, `PySide6`, `pywin32`, `pydirectinput`, `mss` (ou `windows-capture`).

Sem TensorFlow, sem PyTorch, sem Tesseract.

---

## 🗺️ Fases de Desenvolvimento

1. **Visão:** capturar a janela, detetar a malha, desenhar retângulos no overlay. Valida a base inteira.
2. **Assistente:** dHash + memória + números no overlay. **Já é utilizável e entregável por si só.**
3. **Estado:** âncoras de round e tentativas, deteção de fim de round, reset de memória.
4. **Solver:** política de decisão, incluindo o gasto do bónus de linha.
5. **Automático:** execução dos cliques, calibração de timings.
6. **Afinação:** estatísticas por fase, ajuste de limiares, tratamento de casos-limite.

---

## ⚠️ Riscos e Questões em Aberto

**Risco de conta:** automação de input viola os termos do IdleOn e traz risco de ban. O **modo assistente não tem este problema** — é overlay passivo, sem injeção de input, e o jogador é quem clica. O modo automático tem. Decisão consciente do utilizador; o assistente é o caminho seguro e é entregue primeiro.

**A resolver durante o desenvolvimento (não bloqueiam o arranque):**
- Tamanho e escala da janela do jogo, e comportamento com DPI ≠ 100%.
- Duração exata do bloqueio de input após um par errado — define o teto de velocidade do modo automático.
- Valor HSV exato do verde das cartas escondidas.
- Se a arte das cartas se repete entre fases e entre partidas (determina se o catálogo do modo treino compensa).
- Se o bónus de linha revela a linha *inteira* incluindo cartas já emparelhadas/removidas.

---

## 📚 Referências

- OpenCV — máscara HSV, contornos, deteção da malha
- NumPy — dHash e distância de Hamming
- PySide6 — overlay e interface de controlo
- pywin32 — captura de janela, click-through, exclusão de captura
- pydirectinput — injeção de cliques

---

## 💬 Notas Adicionais

**O que este projeto não é.** Não é reconhecimento de imagem difícil e não é machine learning. Arte pixel art estável sobre fundo verde liso é o cenário mais fácil que a visão computacional oferece. O trabalho intelectual está todo na **política de decisão** — sobretudo em onde gastar o bónus de linha, e em perceber que limpar pares conhecidos cedo desperdiça tentativas.

**Cortado da versão anterior deste documento** por não se aplicar ao alvo real: monetização e freemium, suporte mobile, generalização para outros jogos da memória, TensorFlow/PyTorch, OCR/Tesseract, e humanização anti-deteção dos cliques.

---

**Última Atualização:** 2026-08-03
