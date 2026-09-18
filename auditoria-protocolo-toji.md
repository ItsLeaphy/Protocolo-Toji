# Auditoria — Protocolo Toji (site, v2 skate/old-school)

Documento de handoff para o chat principal. Cobre tudo que foi decidido e produzido nesta conversa, do zero até o estado final publicado.

---

## 1. Contexto de entrada

Esta conversa começou a partir de um export de outra conversa (Claude - Treino), que continha:

- O briefing completo de revisão do sistema de treino (perfil, objetivos, filosofia)
- A reconstrução do treino em si, batizado de **Protocolo Toji** (PPL, 6x/semana, teto de 2h30)
- Um primeiro roadmap de execução do site, com conceito "brutalista atlético" (paleta quase monocromática, acento vermelho único, tipografia condensada tipo "ficha de arma")

Ao abrir esta conversa, a pessoa comunicou que **mudou de ideia sobre a direção visual** do site: queria algo "roqueiro, skatista", e perguntou se era viável.

---

## 2. Decisão de direção visual

### 2.1 Pesquisa e embasamento
Antes de fechar qualquer decisão, foi feita pesquisa web sobre:
- Estética grunge/skate nos anos 90 em web design
- David Carson, considerado "pai do grunge" no design gráfico, formado na cultura surf/skate do sul da Califórnia (fim dos 80/início dos 90) — usado como referência raiz legítima, não modinha
- Elementos gráficos de skate deck art e sticker bomb — com a ressalva de que sticker bomb funciona melhor com paleta limitada/temática, não "vale tudo" (senão vira poluição visual)
- Achado histórico relevante: no skate dos anos 90, a caveira substituiu os temas de surf (sol, oceano) como motivo dominante, refletindo uma virada para temas de morte/sobrevivência primitiva

### 2.2 Escolha do sub-estilo
Foram oferecidas 4 opções de sub-estilo dentro de "roqueiro/skatista":
1. Punk/DIY (zine, fita crepe, xerox, colagem)
2. Skate old-school 90s (grunge, deck art, spray, contraste forte)
3. Hardcore/metal (tipografia gótica/stencil, cartaz de show)
4. Street/skate atual (grafite, sticker bomb, cores vibrantes)

**Escolha final: combinação 2 + 4** — base old-school 90s como estrutura, com tempero street atual (sticker, cor viva) como detalhe, não como fundo inteiro.

### 2.3 Três decisões de execução travadas antes de codar
1. **Fundo:** zine claro (papel/creme) — não escuro sujo
2. **Intensidade de textura:** sutil, não crua/agressiva (depois ajustada pra "um pouco mais" a pedido)
3. **Estilo do selo do skill do dia:** redondo, tipo selo de skate shop — não carimbo retangular tipo documento

---

## 3. Roadmap produzido

Um roadmap markdown completo foi criado e entregue como arquivo (`roadmap-treino-skate.md`), cobrindo:
- Paleta de tokens (bg, ink, paper-stain, accent-1/2, cores por tipo de dia)
- Tipografia (Archivo Black para display, Permanent Marker para manifesto, Inter pro corpo, IBM Plex Mono pra dados técnicos)
- Textura e elementos gráficos (grão, bordas irregulares, selo, rabisco)
- Arquitetura da página (hero → nav de abas → painel do dia → apêndice em accordion)
- Regras técnicas (arquivo único self-contained, Google Fonts, sem dependência pesada)
- Ordem de execução em 10 passos

Esse roadmap foi criado originalmente para a pessoa executar em **outra conta** (por questão de tokens), mas a produção real acabou acontecendo nesta própria conversa a pedido posterior da pessoa ("comece a produção").

---

## 4. Produção do site

### 4.1 Abordagem técnica
- Arquivo único HTML self-contained (`protocolo-toji.html`)
- Fontes via Google Fonts (`Archivo Black`, `Permanent Marker`, `Inter`, `IBM Plex Mono`)
- JavaScript puro, sem framework, sem dependência de CDN além das fontes
- Publicado via Artifact do Claude (link: `https://claude.ai/artifact/3WFqjgmAJGjxbB5aiTuNFQ`)
- Dados do conteúdo do treino extraídos com fidelidade total do markdown "Protocolo Toji" original (conferido linha por linha em auditoria posterior)

### 4.2 Estrutura implementada
- **Hero:** título grande desalinhado, frase de manifesto ("harmonia, não hierarquia"), fita no canto (posteriormente virou indicador do dia da semana)
- **Seção "a semana":** tabela com os 7 dias e o tipo de treino de cada um, com chip colorido por categoria (Push/Pull/Legs)
- **Nav de abas:** uma aba por dia (SEG a DOM), cor viva quando ativa, cinza/dessaturada quando inativa
- **Painel de cada dia:** aquecimento, selo redondo do skill (com leve rotação), lista de exercícios em cards expansíveis (papel + RIR + motivo ao clicar), bloco de core quando aplicável, cool-down
- **Apêndice:** accordion com 5 seções (Variantes, Execução e progressão, Postura e respiração, Sobre a cintura, Restrições e dados de partida)

### 4.3 Conteúdo do treino (fiel ao Protocolo Toji original)
| Dia | Treino |
|---|---|
| Segunda | Push A (5 exercícios) |
| Terça | Pull (8 exercícios) |
| Quarta | Legs A + Core A |
| Quinta | Push B (5 exercícios) |
| Sexta | Legs B + Core B |
| Sábado | Pull (repete terça, variantes diferentes) + ciclismo 32km |
| Domingo | Descanso |

---

## 5. Ciclo de revisão e ajustes

### 5.1 Primeiro ajuste: intensidade do grão
Pedido: aumentar o grão da textura (estava sutil demais). Ajustado de opacidade 0.045 para 0.11 — depois mantido nesse valor pelo resto do projeto.

### 5.2 Segundo ajuste: informação faltando
A pessoa relatou uma sensação de "falta informação" sem saber apontar exatamente o quê. Comparação linha por linha com o markdown revelou 3 buracos reais:
1. Vários campos de `detail` (motivo do exercício) estavam vazios nos dias de Pull (terça/sábado) e na panturrilha de quarta — cards abriam sem explicação
2. Faltava um parágrafo de contexto/lógica no topo de cada painel de dia (por que aquele dia é A/B, por que repete, etc.) — essa lógica só existia na seção "a semana", não dentro de cada dia individual
3. (Mencionado mas explicitamente fora de escopo: BLOC não precisava ser integrado ao site)

**Ação:** todos os `detail` vazios foram preenchidos com explicações reais extraídas/inferidas do contexto do markdown; foi adicionado um campo `intro` por dia, renderizado no topo de cada painel.

### 5.3 Terceiro ajuste: confusão nas variantes (especialmente terça)
Problema identificado: informação de variante estava **duplicada** — cada card de exercício já dizia "Terça: X" / "Sábado: Y" dentro do próprio detail, e uma tabela comparativa embaixo repetia os mesmos 4 exercícios comparando os dois dias, causando confusão sobre se era informação nova ou repetida.

**Ação:**
- Removido o prefixo redundante ("Terça:", "Sábado:") dos cards — cada dia agora só mostra a variante daquele dia, sem repetir o nome do dia
- A tabela comparativa terça x sábado foi movida para dentro do accordion "Variantes" no apêndice — lugar correto para comparação entre dias, não dentro do painel de um dia específico

### 5.4 Quarto ajuste: revisão completa contra o MD
Pedido explícito de garantir que nenhuma informação estivesse fora do lugar. Foi feita conferência exaustiva, exercício por exercício, RIR por RIR, de todos os 7 dias contra o markdown original de 2780 linhas. Resultado: tudo conferido e correto, nenhuma divergência encontrada além do problema de duplicação já corrigido no item 5.3.

### 5.5 Quinto ajuste: remoção de código morto
Pedido: remover código morto e garantir que nada quebrasse. Identificado um bloco JS (`if (d.variantTable)`) que nunca mais disparava desde a mudança do item 5.3, pois nenhum dia mais possuía essa propriedade. Removido.

**Validações de segurança realizadas:**
- Sintaxe JS checada com `node --check` — sem erros
- Balanceamento de chaves/parênteses/colchetes conferido programaticamente
- Todos os `getElementById` usados no JS confirmados como existentes no HTML
- Todas as funções definidas confirmadas como usadas/chamadas corretamente

### 5.6 Análise profunda solicitada
Foi pedida uma auditoria/veredito sobre código, informação e estética do projeto até aquele ponto. Veredito dado: código sólido e sem gambiarra, informação fiel ao MD sem invenção, estética coerente com a referência real pesquisada (não "vibe dark genérica de IA"). Ressalvas honestas: responsividade testada apenas por inspeção de código (sem acesso a browser real no ambiente), acessibilidade não auditada a fundo, BLOC intencionalmente não integrado.

---

## 6. Três últimas features implementadas

### 6.1 Dark mode com ícone (sem texto)
- Botão circular fixo no canto inferior direito, com ícone SVG de sol/lua (sem nenhum texto/label)
- Alterna entre o tema zine claro original e uma paleta escura equivalente (fundo quase preto `#17140F`, tinta clara `#EDE6D6`, acentos mais vivos para compensar o contraste)
- Preferência persistida via `localStorage`
- Textura de grão ajustada para se comportar bem em ambos os temas (`multiply` no claro, `screen` no escuro, com opacidades diferentes)

### 6.2 PWA — "instalar no celular"
- Manifest gerado dinamicamente em runtime (via `Blob` + `URL.createObjectURL`), já que um arquivo único HTML não pode referenciar um `manifest.json` externo separado
- Service worker mínimo (cache-first) registrado da mesma forma, via Blob
- Meta tags de PWA adicionadas (`theme-color`, `apple-mobile-web-app-capable`, ícones em SVG inline)
- **Ressalva importante comunicada à pessoa:** isso não funciona dentro do preview do Claude Artifact (ambiente sandboxed/iframe) — só funciona quando o arquivo for hospedado num domínio real com HTTPS. A pessoa confirmou que queria isso pronto mesmo assim, para quando hospedar em outro lugar.

### 6.3 Tape do hero vira dia da semana + auto-seleção de aba
- A tape que antes mostrava texto fixo ("SET / 2026 — V2") agora mostra o dia da semana atual (ex: "SEX"), calculado via `Date().getDay()` no carregamento da página
- A aba correspondente ao dia atual é automaticamente selecionada ao abrir a página, sem exigir clique
- Validado que a ordem de inicialização no JS está correta (abas e painéis são construídos antes da tentativa de auto-seleção, evitando erro de elemento inexistente)

---

## 7. Estado final

- **Link do artifact publicado:** `https://claude.ai/artifact/3WFqjgmAJGjxbB5aiTuNFQ`
- **Arquivo:** `protocolo-toji.html`, single-file, self-contained
- Todas as validações de sintaxe e integridade estrutural passaram
- Conteúdo do treino 100% fiel ao Protocolo Toji original
- Direção visual: skate old-school 90s + street atual, zine claro, com dark mode opcional
- PWA pronto para funcionar assim que hospedado externamente

### Pendências conhecidas (não resolvidas nesta conversa, por decisão explícita ou por estarem fora de escopo)
- Integração com o BLOC (app de registro de treino) — explicitamente fora de escopo a pedido da pessoa
- Teste em dispositivo real / browser real — não foi possível neste ambiente (sem acesso de rede para instalar browser headless)
- Auditoria de acessibilidade (contraste, navegação por teclado) — não realizada a fundo
- Responsividade mobile — só um breakpoint (600px) implementado, não testado visualmente em dispositivo
