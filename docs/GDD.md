# GDD 05 — SCRAPSTORM
## Survivor-like / Action Casual / Portrait / Android + iOS

> **Revisão 2026-10-09 (comparativo de mercado):** detalhe, fontes e matriz em [`COMPETITIVO.md`](COMPETITIVO.md).
> - **Os dois ganchos originais já têm dono.** "Monte seu mech" é o Mech Assemble (ONEMT; receita estimada em ~US$170K/dia, não confirmada; caixas de recompensa pagas). "Extraia ou arrisque" está sendo testado pela Voodoo (Last Extract, 02/2026) e por indies. Nenhum deles liga o saque ao corpo do mech.
> - **Core revisto (§2):** a sucata carregada vira **placas de blindagem** no mech. Saque = armadura = isca: o golpe arranca placas (recolhíveis por 3 s), e quanto mais placas, mais inimigos. Extrair converte as placas em sucata guardada.
> - **A extração deixa de ser conta de valor esperado (§2):** a tempestade fecha a arena em blocos de ~2,5 min, e extrair exige 5 s de exposição com densidade proporcional às placas. A run passa a ter mediana de 4–5 min e teto de 8 min.
> - **FTUE corrigida (§3):** a 1ª run termina numa extração guiada, e o hangar mostra o que a sucata compra antes da 1ª escolha de verdade.
> - **Economia e monetização nos guardrails (§6, §7):** 1 moeda no MVP (Cores e Blueprints saem do MVP), sem energia, sem item aleatório pago, baú com conteúdo visível, interstitial desligado na v0.1, rewarded com id de transação.
> - **KPIs e kill criteria alinhados ao veredito (§15, §26):** D1 ≥26%, D7 ≥5%, coorte de 1,5–2 mil installs, cancelar só após 2 iterações. Os valores anteriores (28% / 7%, cancelar por D1 sem qualificador) ficavam acima do top quartil.
> - **Reuso do ARKANA corrigido (§13, §23)** para o que existe em disco; estava contado duas vezes no ranking.
> - Seções novas: **§27 Diferenciais competitivos** e **§28 Hipóteses de protótipo e catálogo de exploits**. Veredito mantido: **depois** (só após um puzzle ou idle validar).

> **Hipótese comercial:** um action casual de runs curtas, com movimentação de um dedo e montagem visual do mech durante a partida, pode aproveitar tecnologia de ARKANA e criar UA forte sem o custo de multiplayer competitivo.

# 1. VISÃO DO PRODUTO

**Nome:** Scrapstorm  
**Gênero:** survivor-like / action casual / light extraction  
**Plataforma:** Android primeiro.  
**Orientação:** Portrait.  
**Público:** 13–40, action casual, Archero/survivor-like, roguelite leve.  
**Proposta:** sobreviver em arenas de sucata viva enquanto módulos se encaixam fisicamente no mech.  
**Fantasy:** começar frágil e improvisar uma máquina absurda antes da tempestade destruir tudo.  
**Diferencial:** upgrades aparecem fisicamente no mech e o jogador escolhe extrair cedo ou continuar arriscando.

**Diferencial revisado (2026-10-09):** a sucata que você carrega aparece como placas no mech e é ao mesmo tempo armadura, saque e isca; a tempestade obriga a decidir quando sair. O encaixe de módulos continua, mas sozinho já é território do Mech Assemble (ver `COMPETITIVO.md`).

# 2. GAMEPLAY

## Core mechanic
- joystick virtual de um dedo;
- auto-fire no alvo mais próximo válido;
- dodge cooldown curto;
- drops de XP/scrap;
- escolha de 1 entre 3 módulos em milestones;
- extração opcional após checkpoints.

## Tipos de módulo
- arma frontal;
- drone;
- escudo;
- trilho elétrico;
- saw/close-range;
- capacitor;
- dash mod.

## Core loop
`entrar → mover → sobreviver → escolher módulo → formar build → extrair/arriscar → hangar → nova run`

## Vitória
Sobreviver ao boss final ou extrair com sucesso.

## Derrota
Perde parte do scrap não protegido; progressão principal nunca zera totalmente.

## Sessão típica
6–10 min.

Revisado em 2026-10-09: blocos de ~2,5 min, mediana-alvo de 4–5 min, teto de 8 min (ver abaixo).

## Revisão 2026-10-09: sucata-blindagem e tempestade (PROPOSTA)

Motivo: a raia B mostrou que o módulo encaixado é só visual e que "100% agora × 2× depois" vira conta de valor esperado em 3–4 runs. A pesquisa mostrou que "mech que cresce" e "extração" já têm dono, cada um separado. A junção dos dois é o que ninguém faz.

**Regras (valores iniciais; calibrar no bot):**
1. **Placas.** Cada sucata recolhida vira uma placa encaixada num soquete livre do mech, que cresce e fica mais pesado (-1,5% de velocidade por placa, teto de -20%). Até 24 placas visíveis; acima disso, contador.
2. **Golpe arranca placas.** Cada golpe tira 1 placa antes de tocar no casco (golpe pesado: 3). As placas se espalham e podem ser recolhidas por 3 s; depois, somem.
3. **Calor.** A densidade de inimigos cresce com as placas carregadas (ponto de partida: +3% de spawn por placa).
4. **Blocos de tempestade.** A run tem até 3 blocos de ~2,5 min e o boss. No fim de cada bloco, a frente da tempestade fecha ~1/3 da arena e uma cápsula de extração cai num ponto visível, longe do jogador.
5. **Extrair.** Ficar 5 s no círculo da cápsula com o calor no máximo. Ao concluir, a run termina e todas as placas viram sucata guardada (1:1).
6. **Continuar paga mais.** Cada bloco seguinte paga mais sucata por inimigo (x1 → x1,5 → x2) e a tempestade aperta. O boss só aparece para quem não extraiu nos 3 blocos.
7. **Morrer.** Perde 70% das placas carregadas; 30% é sucata protegida (o rewarded "double protected scrap" de §7 dobra essa parte).
8. **Módulos (1 de 3)** continuam como estão: fixos na run e visíveis, sem relação com as placas.
9. **Interrupção.** Se o app for para segundo plano, a run pausa e grava o estado; reabrir retoma do mesmo ponto, sem restaurar placa perdida.

**Feedback:** som e haptic distintos para placa encaixando, placa caindo e placa recolhida; contorno pulsante no mech quando o calor passa de 75%.
**Falha:** perder placas é a falha pequena; morrer com placas é a grande. A meta nunca zera.
**Teste:** §28 (H1–H3).

# 3. PRIMEIROS 10 MINUTOS

**0:00–0:30** — mech cai numa arena, tutorial só de movimento. Arma dispara sozinha.

**0:30–1:20** — primeiros inimigos fracos; XP enche rápido.

**1:20–2:00** — escolha de primeiro módulo: drone / shotgun / shield. O módulo aparece no corpo do mech.

**2:00–3:00** — densidade cresce; primeiro dodge contextual.

**3:00–4:00** — miniboss simples; drop visual de scrap.

**4:00–5:00** — checkpoint de extração: “sair com 100% do scrap ou continuar por 2× recompensa potencial”.

**5:00–6:30** — jogador continua por padrão sugerido no primeiro run; recebe segundo módulo.

**6:30–8:00** — elite com telegraph claro. Primeira quase-morte.

**8:00–9:00** — boss tutorial; vitória não precisa ser garantida, mas curva deve ser generosa.

**9:00–10:00** — hangar: gastar scrap em sidegrade leve/slot de blueprint; primeira reward chest. Rewarded opcional para duplicar parte do scrap.

### FTUE revisada (2026-10-09): esta é a que vale

A sequência acima é a original. Ela oferecia a extração aos 4 min, antes de o jogador saber quanto vale a sucata, e sugeria continuar por padrão (raia B).

**Run 1 (~3 min; sem morte possível no bloco 1):**
- **0:00–0:30:** o mech cai pequeno; tutorial só de movimento; a arma dispara sozinha.
- **0:30–1:20:** inimigos fracos; cada sucata recolhida vira uma placa no corpo (o hook visual acontece no 1º minuto).
- **1:20–2:00:** 1ª escolha de módulo (drone / shotgun / shield); o módulo aparece no corpo.
- **2:00–2:30:** o 1º golpe forte arranca placas; o jogo mostra o ímã de 3 s para recolher.
- **2:30–3:00:** a tempestade fecha a borda e a cápsula cai; **extração guiada** (na run 1 só existe essa opção).
- **Hangar (1ª vez):** a sucata guardada compra na hora o 1º sidegrade, para o jogador saber quanto ela vale antes de arriscar.

**Run 2 (~4–6 min):**
- **0:00–2:30:** bloco 1; 2º módulo.
- **2:30:** 1ª escolha real: extrair (5 s exposto) ou seguir para o bloco 2, que paga x1,5.
- **2:30–5:00:** bloco 2; elite com telegraph claro; 1ª quase-morte provável.
- **5:00:** 2ª cápsula. Quem continuar enfrenta o bloco 3 e o boss tutorial (curva generosa).
- **Fim:** hangar. Na v0.2, rewarded opcional para dobrar a sucata protegida (§7). Sem interstitial.

# 4. PRIMEIRO DIA

- 3 arenas;
- 12 módulos;
- 6 inimigos;
- 3 elites;
- 2 bosses;
- 2 chassis;
- 15 upgrades meta laterais;
- 1 daily challenge.

Primeiro rewarded depois da primeira run.
Primeiro IAP: Remove Ads/Starter Salvage Pack após 2–3 runs.

Retorno:
- daily blueprint;
- challenge do dia;
- próximo chassis.

# 5. PROGRESSÃO

Curta: módulos durante run.  
Média: blueprints/chassis.  
Longa: mastery, challenge modes e novos biomas.

D1: 4–6 runs.  
D3: segundo chassis.  
D7: bioma 2 e challenge.  
D14: modifier runs.  
D30: season-lite.  
D60: novo weapon family.  
D90: event variants.

# 6. ECONOMIA

**Scrap:** soft currency.
Fontes:
- run;
- extraction;
- quest;
- rewarded.

Sinks:
- unlock lateral;
- reroll controlado;
- hangar convenience.

**Cores:** hard currency.
Usos:
- cosmetics;
- bundles;
- challenge retry opcional.

**Blueprints:** gameplay progression.

Evitar upgrade permanente que torne gameplay trivial. Meta deve abrir variedade, não multiplicar poder indefinidamente.

### Ajuste 2026-10-09 (guardrails do portfólio)
- **1 moeda no MVP: Sucata (Scrap).** Cores (hard currency) saem do MVP e só voltam na v1.0 se a coorte justificar. Blueprints deixam de ser moeda e viram desbloqueios comprados com sucata.
- **Mapa de fontes e ralos (MVP):**

| Fonte | Teto/controle | Ralo |
|---|---|---|
| Extração (placas → sucata 1:1) | calor e duração da run (≤ 8 min) | sidegrades laterais (preço crescente por linha, teto de 5 níveis) |
| Sucata protegida na morte (30%) | só da run atual | reroll de módulo (1 grátis por run; os demais por rewarded) |
| Quest diária | 1 por dia, id de transação `quest-AAAAMMDD` | desbloqueio do 2º chassi |
| Rewarded "dobrar sucata protegida" (v0.2) | 1×/run, id de transação por run | — |

- **Retorno decrescente:** nenhum conjunto de sidegrades soma mais de +15% de dano bruto; a meta abre variedade, não poder.
- **Relógio do aparelho:** a data só libera a quest do dia; voltar o relógio não libera de novo (o jogo guarda a última data vista). Progressão nunca depende do relógio.
- **Offline:** não se aplica (não há renda passiva).

# 7. MONETIZAÇÃO

Rewarded:
- revive 1x/run;
- double protected scrap;
- reroll module;
- daily crate.

Interstitial:
- entre runs, cap forte;
- nunca durante combate.

IAP:
- Remove Ads;
- Starter Pack;
- cosmetics/chassis skins;
- cores;
- event pack.

Sem venda de “best weapon”.

### Ajuste 2026-10-09 (guardrails e posicionamento)
- **v0.1:** sem anúncio e sem IAP. **Interstitial desligado** na v0.1; se entrar depois, só entre runs, nunca nas 3 primeiras runs do dia, com cap forte.
- **Rewarded (v0.2):** revive 1×/run, dobrar a sucata protegida, reroll de módulo. Cada concessão tem id de transação (`rw-<runId>-<tipo>`) e não se repete se o app for fechado e reaberto.
- **O "daily crate" vira caixa do dia com conteúdo visível antes de abrir.** Nenhum item aleatório pago, nem por moeda (ECA Digital, Lei 15.211/2025).
- **IAP no MVP:** só Remove Ads e Starter Pack de conteúdo fixo e listado. Cores, cosméticos e event pack ficam para a v1.0, sempre com conteúdo fixo.
- **Posicionamento:** "sem energia, sem gacha" na página da loja e no cartão final dos criativos (§27, D4).
- **Expectativa honesta:** o gênero monetiza vendendo poder por sorteio (Archero 2, Mech Assemble). Sem isso, o teto de IAP é baixo, e a receita depende de rewarded e de CPI ≤ US$0,90 (raia B; `COMPETITIVO.md`).

# 8. RETENÇÃO

D1: build discovery.
D3: chassis.
D7: biome/challenge.
D14: modifier.
D30: mastery/cosmetics.

Daily quests:
- use module family;
- extract after X checkpoint;
- kill elite.

# 9. LIVE OPS

- Overclock Weekend;
- Drone Week;
- Boss Rush;
- Toxic Scrapstorm;
- Extraction Challenge.

Events reutilizam inimigos/arenas com modifiers.

# 10. CONTEÚDO

MVP:
- 1 arena;
- 6 modules;
- 4 enemy types;
- 1 elite;
- 1 boss;
- 1 chassis.

Lançamento se validado:
- 4 biomes;
- 30–40 modules;
- 20 enemy types;
- 8 bosses;
- 6 chassis;
- 5 event templates;
- 30 cosmetics.

# 11. ARTE

Stylized sci-fi salvage.
Silhuetas simples, VFX fortes, materiais baratos.
Módulos encaixáveis fisicamente são o principal hook visual.

# 12. ÁUDIO

- auto-fire;
- impact;
- pickup;
- level-up;
- module attach;
- dodge;
- shield break;
- extract;
- boss.

Haptic em hit pesado/module attach.

# 13. TECNOLOGIA

Unity/C#.

Reuso direto de ARKANA:
- touch movement;
- projectile pooling;
- hit/damage;
- bots/enemy steering simplificado;
- performance profiling;
- animation/VFX patterns.

Arquitetura:
- `RunDirector`
- `EnemySpawner`
- `AutoTargeting`
- `ProjectileSystem`
- `ModuleSystem`
- `BuildRuntime`
- `ExtractionSystem`
- `MetaProgression`
- MobileCore.

### Reuso real (verificado pela raia C em 2026-10-06)
A lista acima superestima o reuso, que estava contado duas vezes no ranking (Reuso 10 e Facilidade 7; a raia D corrigiu para 7 e 6). O que serve de fato, em `ARKANA/mobile-unity/Assets/_Arkana/Scripts/`:
- `UI/JoystickVirtual.cs` (`JoystickLogica` pura, mas depende de `Arkana.Core`: desacoplar);
- `Gameplay/Projetil.cs` (voo puro; depende de `Elemento`/`ArmaSpec`: desacoplar);
- o pool em `Gameplay/VisualDoAbate.cs`, mais `BancadaDeCortes.cs` e `MedidorDeFps.cs` (FPS medido no aparelho);
- `UI/AreaSegura.cs`, `UI/Dp.cs` e `UI/Formas.cs` (a raia C já os indicou para o Rune Relay).

**Não serve:** `Gameplay/Bot.cs` (57 referências a Sintonia, Elemento e Zona). **Não existe e precisa ser escrito:** horda com hash espacial e pool (150+ inimigos, sem `Physics` por inimigo), câmera retrato, Ads/IAP e a simulação headless da run em passo fixo, que serve ao bot de balance, à semente determinística (§27, D6) e à gravação de criativos por autoplay.

# 14. ANALYTICS

- run_start/end
- run_duration
- death_cause
- extraction_offer/choice
- module_offer/choice
- module_synergy
- damage_source
- revive_offer/complete
- boss_start/end
- currency_source/sink
- iap_view/purchase
- fps_bucket/device_tier

Métricas:
- run 1 completion;
- second-run start;
- avg runs/day;
- D1/D7;
- chosen module diversity;
- ad opt-in;
- CPI.

Eventos acrescentados em 2026-10-09: `plate_gained`, `plate_lost`, `plate_recovered`, `heat_level`, `storm_block_start`, `extraction_window` (bloco, placas carregadas, vida), `extraction_result`, `seed_code_entered`, `share_card`.

# 15. KPIs — TARGETS INTERNOS

- tutorial completion ≥88%;
- first run reaches first extraction ≥80%;
- second run started same session ≥55%;
- D1 ≥26% (era 28%; alinhado ao veredito de 2026-10-06);
- D3 ≥12% (acompanhamento, não é gate);
- D7 ≥5% (era 7%; o top quartil do GameAnalytics 2026 fica em 6–7%);
- D30 ≥1,5% (acompanhamento);
- avg 3+ runs/day nos retidos;
- rewarded opt-in ≥35%;
- crash-free >99.5%.
- **Gate de receita na fase B (IAA, não payer):** opt-in de rewarded, impressões de rewarded por DAU e ARPDAU. Payer conversion só a partir de 5 mil installs.
- **Coorte:** 1,5–2 mil installs pagos em geo barata (BR/PH/ID), sempre comparando pago com pago.

UA low-cost action:
- CPI ≤ ~US$0,90 promissor;
- 0,90–1,40 iterar;
- >1,40 exige LTV excepcional.

# 16. TESTE DE MERCADO

Creative-first:
- “mech grows visibly”;
- “bad build vs broken build”;
- “extract or risk”.
- “saque no corpo”: o mech cresce com placas e as perde no golpe (§27, D1);
- controles: “mech que só cresce” (estilo Mech Assemble) e survivor genérico.

1.500–2.000 installs Android (revisado em 2026-10-09: com 1 mil installs, a margem do D7 é de ±1,7 pp).
Amostra device mix ampla por performance.

# 17. 10 CRIATIVOS UA

1. mech minúsculo → cheio de módulos em 15 s;
2. escolha errada de módulo → morte;
3. “extract now or risk 3×?”;
4. drone swarm build;
5. shield build sobrevivendo a boss;
6. 1 HP extraction;
7. boss telegraph → dodge perfeito;
8. “qual dos 3 upgrades?”;
9. build visual absurda;
10. comparação chassis A/B.

Acrescentados em 2026-10-09 (§27):
11. mech gigante leva golpe → placas voam → corre para recolher → cápsula a 3 s;
12. tempestade fechando + “extrair com 2 placas ou entrar no bloco x2?”;
13. cartão final “sem energia, sem gacha” (A/B com e sem).

# 18. MVP

- one-thumb movement;
- auto-target/fire;
- 1 arena;
- 6 modules;
- 1 boss;
- extraction;
- sucata-blindagem (placas) e tempestade em blocos (§2, revisão 2026-10-09);
- simulação em passo fixo com semente (base do código de desafio da v0.2);
- analytics;
- Android;
- 8 criativos.

Sem:
- online;
- guild;
- PvP;
- battle pass;
- 40 modules.

# 19. V0.1

Core combat + one run, já com placas e tempestade (§2). Sem anúncio e sem IAP.

# 20. V0.2

Se marketability/feel passarem:
- 2 arenas;
- 12 modules;
- meta;
- ads/IAP;
- remote config;
- código de desafio e cartão de ferro-velho (§27, D5–D6).

# 21. V1.0

Se D7/LTV:
- 4 biomes;
- 30+ modules;
- events;
- iOS;
- localization.

# 22. PRODUÇÃO

| Área | Peso |
|---|---|
| Programação | Médio |
| Design | Médio–Alto |
| Arte | Médio |
| UI | Médio |
| Áudio | Médio |
| Backend | Baixo |
| Analytics | Médio |
| Conteúdo | Médio |

Complexidade: **6/10**.

# 23. REUTILIZAÇÃO

ARKANA é principal fonte:
- movement;
- projectile;
- hit detection;
- bots;
- VFX;
- device lab.

COE:
- save;
- progression patterns.

MobileCore compartilhado.

**Correção 2026-10-09:** ver "Reuso real" em §13. Do ARKANA servem joystick, projétil, pool e a bancada de FPS; bots, detecção de acerto e VFX precisam ser escritos. Do COE, o padrão de save e o de combate (`Health`, `Damage`, `Hitbox`).

# 24. IA

- module concepts;
- enemy silhouettes;
- balance simulation;
- test agents;
- UA storyboard;
- code/test assistance;
- localization.

Não runtime.

# 25. RISCOS

**Parece Archero/Survivor genérico.**  
Visual attach + extraction decision precisam ser centrais.

**Performance com hordas.**  
Pooling, cap, LOD, simple AI.

**Meta vira pay-to-win contra PvE.**  
Priorizar sidegrades.

**Runs longas.**  
Meta 6–10 min.

**Os ganchos já têm dono (2026-10-09).**
O Mech Assemble faz "monte seu mech"; o Last Extract (Voodoo) e indies fazem "extraia ou arrisque". Só a junção (o saque no corpo) é nossa. Mitigação: testar o hook D1 contra esses controles antes de construir (§27, §28).

**Receita sem sorteio pago.**
Os líderes vendem poder por gacha e caixa, vedados para nós (ECA Digital). Mitigação: CPI ≤ US$0,90 em geo barata, rewarded bem colocado e o posicionamento "sem energia, sem gacha".

**Frustração ao perder placas.**
Mitigação: ímã de 3 s, 30% de sucata protegida na morte e teto de placas visíveis.

# 26. KILL CRITERIA

> Revisado em 2026-10-09 para o padrão do veredito: coorte de 1,5–2 mil installs e cancelamento só após 2 iterações estruturais. A versão anterior pedia D1 ≥28% e D7 ≥7% para continuar (acima do top quartil) e cancelava por D1 <22% sem qualificador.

## CONTINUAR
- second run start ≥55%;
- D1 ≥26%;
- D7 ≥5%;
- CPI dentro do target (≤ ~US$0,90);
- jogadores citam as placas/tempestade (o saque no corpo) como diferencial sem serem perguntados;
- 30 FPS de piso nos aparelhos-alvo mínimos do teste.

## ITERAR
- D1 20–26%;
- D7 3,5–5%;
- CPI até 50% acima;
- combate divertido mas upgrades repetitivos;
- extrações concentradas num só ponto (>60%): a decisão não está funcionando;
- boa retenção em high-end, performance ruim em mid-tier.

## CANCELAR (só após 2 iterações, cada uma com coorte de 1,5–2 mil installs)
- second run start <40%;
- D1 <20% (mediana do GameAnalytics 2026);
- D7 <3,5%;
- CPI >2× o target em 8–10 criativos;
- o hook "saque no corpo" (§27, D1) não bate o controle "mech que só cresce" em CPI: o jogo não tem ângulo próprio;
- performance inviável sem reduzir hordas a ponto de perder a fantasia.

# 27. DIFERENCIAIS COMPETITIVOS (revisão 2026-10-09)

Resumo. O detalhe (por que importa, como funciona, custo, risco e validação) e as fontes estão em [`COMPETITIVO.md`](COMPETITIVO.md). Tudo é **PROPOSTA**. Custo: P ≤ 1 semana, M 2–4 semanas, G ≥ 1 mês.

| # | Diferencial | O que nenhum similar pesquisado tem | Custo | Quando |
|---|---|---|---|---|
| D1 | **A sucata é a blindagem** | o saque carregado fica no corpo do mech como armadura e isca (§2) | M | **1º**, no MVP |
| D2 | **A tempestade é o relógio** | extração com exposição, em blocos de ~2,5 min (§2) | P–M | **2º**, no MVP |
| D4 | **Sem energia, sem gacha** | justiça como promessa na loja e no anúncio (§7) | P | **3º**, já no teste de criativos |
| D3 | Run de bolso | mediana de 4–5 min; pausa e grava ao ir para segundo plano | P | junto com D2 |
| D5 | Cartão de ferro-velho | imagem da build pronta para o WhatsApp | P | v0.2 |
| D6 | Desafio por código | semente de 6 caracteres, sem backend | P–M | base no MVP, botão na v0.2 |
| D7 | Escolta de carga | modo futuro com o mesmo kernel de ação | M | v1.0, se validar |

**Por que estes três primeiro:** D1 é a identidade (sem ele o jogo é "Mech Assemble sem gacha"); D2 conserta a extração que virava conta de valor esperado; D4 custa zero, é exigência legal e ataca a maior reclamação dos líderes.

**Posicionamento (rascunho):** o survivor de bolso em que o saque que você carrega vira a armadura do seu mech, e a tempestade decide quando é hora de sair.

# 28. HIPÓTESES DE PROTÓTIPO E CATÁLOGO DE EXPLOITS (2026-10-09)

Cada hipótese tem métrica, protocolo e critério de refutação. Nenhuma está validada.

| # | Hipótese | Protocolo | Refutada se |
|---|---|---|---|
| H1 | O hook "saque no corpo" baixa o CPI frente a "mech que só cresce" | lote de 8–10 criativos, mesmos geos e orçamento | CPI do D1 ≥ CPI do controle |
| H2 | A extração vira decisão, não conta | bot: 2 bases de semente × 30 runs por política; playtest com 5–8 pessoas | uma política fixa rende >15% acima da adaptativa, ou um ponto concentra >60% das extrações |
| H3 | Perder placas é tenso, não frustrante | playtest com pergunta pós-run + `plate_recovered`/`plate_lost` | menos de 40% das placas derrubadas são recolhidas, ou a maioria chama de "injusto" |
| H4 | A run de bolso segura a 2ª run | telemetria `second_run_start` | 2ª run na mesma sessão <45% |
| H5 | Horda + placas cabem em 30 FPS no aparelho-alvo mínimo | `BancadaDeCortes`/`MedidorDeFps` com 150 inimigos e 24 placas | piso <30 FPS (33 ms por quadro) sem cortar a horda pela metade |

**Catálogo de exploits (cada um vira teste nomeado):**
- **Fechar o app antes de morrer** para não perder placas → a run grava o estado ao ir para segundo plano e retoma do mesmo ponto; reabrir nunca restaura placa perdida.
- **Rewarded repetido** (fechar e reabrir na tela de recompensa) → id de transação por run e tipo; a 2ª concessão com o mesmo id é ignorada.
- **Farm no 1º bloco** (extrair sempre aos 2,5 min) → a sucata por minuto tem de crescer com a profundidade (H2).
- **Voltar o relógio** para repetir a quest diária → o jogo guarda a última data vista; data anterior não libera nada.
- **Repetir a mesma semente** (código de desafio) para farmar → partida por código não paga sucata; vale só o placar.
- **Save antigo ou de versão futura** → migração explícita v0→v1; versão futura é recusada sem apagar o save.

---

## Lições do estúdio aplicadas a Scrapstorm (do Dungeon Courier, 2026-10-16)

O Dungeon Courier (DC) foi do GDD à 1.4.1-beta com núcleo testado fora do Unity, arte v2, tutorial guiado, anúncios e compras, AAB assinado e política pública; cada lição abaixo foi paga lá com tempo, crédito ou retrabalho. O playbook completo está em [`docs/LICOES_PARA_O_ESTUDIO.md`](https://github.com/Vvs2705/dungeon-courier/blob/main/docs/LICOES_PARA_O_ESTUDIO.md) (repositório `Vvs2705/dungeon-courier`), com cópia na memória do estúdio em `C:\Users\VINICIUS\Videos\MEUS PROJETOS\Agentes\_memoria\PLAYBOOK_ESTUDIO_DUNGEON_COURIER.md`. O DC é o parente mais próximo do Scrapstorm no estúdio: ação de um dedo em retrato, ataque automático, inimigos com chefes, simulação com semente e bot. Boa parte do que o §13 e o §23 esperam do ARKANA já existe no DC, desacoplada. Status de tudo: **PROPOSTO**. Caminhos marcados "DC" são do repositório `dungeon-courier`; "Forge", de `03_FORGE_STREET`; "ARKANA", de `ARKANA/mobile-unity/Assets/_Arkana/Resources/`. Clipes Mixamo ficam fora do git, no checkout principal. A reutilização entre projetos tem aval do Vinicius de 2026-10-09 (cópia, sem alterar a origem). Formato de cada item: **o que fazer** · **por quê** (o que aconteceu no DC) · **reaproveitar**.

### Processo
- **Contrato da v0.1 antes do 1º código.** **O que fazer:** escrever `docs/CONTRATO_V01.md` com o escopo do §18–19 (1 arena, 6 módulos, 4 inimigos, 1 elite, 1 chefe, placas e tempestade, simulação com semente) e os números das "Regras" do §2 como hipóteses que o bot mede em `docs/BALANCE.md`. Depois, `docs/CONTRATO_LANCAMENTO.md` com a matriz "seção do GDD × feito". **Por quê:** no DC, o contrato escrito antes deixou núcleo e View andarem em paralelo, e a matriz é o que diz "pronto". **Reaproveitar:** DC `docs/CONTRATO_V01.md` (a §2 já define o contrato Core ← View de um jogo de um dedo) e `docs/CONTRATO_LANCAMENTO.md` §1.
- **Memória de retomada.** **O que fazer:** ao começar o código, criar `scrapstorm.md` e `STATUS_scrapstorm-v01.md` em `Agentes\_memoria\`, com um bloco "CONTINUAR DAQUI" a cada pausa. **Por quê:** o Vinicius retoma dizendo só "vamos continuar"; sem esse bloco, cada sessão reabre a investigação.
- **Fotos antes do PR.** **O que fazer:** foto `-shot` de cada tela e de momentos de combate (mech com 24 placas, horda cheia, placas caídas, tempestade fechando). **Por quê:** no DC, as fotos pegaram o joystick tampando o personagem e texto sobreposto, e nenhum dos 169 testes verdes pegou isso. Aqui, o risco é a poluição visual em tela pequena (§27 D1).
- **Um processo pesado por vez.** Render do elenco no Blender e Unity nunca juntos (PC de 7,7 GB); render em segundo plano e com `timeout` (no DC, um render travou 15 h com o PC suspenso).
- **Proveniência desde o 1º asset**, em `docs/PROVENIENCIA.md` (DC `docs/PROVENIENCIA.md` §1 e §6 como modelo).

### Código e testes
- **Esqueleto copiado, não reescrito.** **O que fazer:** copiar a estrutura `Scripts/Core` (asmdef com `noEngineReferences`), `Scripts/View`, `Editor/Setup.cs`, `Tests/EditMode`, `client/tools/coretests`, `client/tools/viewcheck` e o CI do núcleo, trocando `DC` por `SS`. **Reaproveitar:** DC `client/Assets/_DC/Scripts/Core/DC.Core.asmdef`, `client/Assets/_DC/Editor/Setup.cs`, `client/tools/coretests/DCCore.Tests.csproj`, `client/tools/viewcheck/`, `.github/workflows/nucleo.yml`.
- **Núcleo determinístico em passo fixo de 1/30 s, com xorshift e semente.** **O que fazer:** fazer do `Sim` a fachada, com `Tick(dt, move, dodge)` e a API documentada no topo; a View só desenha o estado e lê `Sim.Events`. Isso é o que o §13 ("simulação headless da run em passo fixo") e o §27 D6 (desafio por código) pedem. **Por quê:** no DC, foi o que permitiu 169 testes, bot e balance fora do Unity, e o determinismo custa caro se for adaptado depois. **Reaproveitar:** DC `client/Assets/_DC/Scripts/Core/Sim.cs` (`Tick(float dt, V2 move, bool dash)`), `Run.cs`, `Defs.cs` e o vetor `V2` próprio. É novo, e o DC não tem: a horda de 150+ inimigos com hash espacial e pool.
- **Bot e `-autoplay N` para a H2.** **O que fazer:** um bot com semente e 3 políticas de extração ("sempre no 1º bloco", "nunca", "adaptativa por placas × vida"). `-autoplay` imprime a sucata por minuto por bloco, a % de extração por ponto, as mortes e as placas recolhidas, mais o teste "mesma semente 2× = mesmo resultado" (D6). **Por quê:** no DC, o bot mediu o balance e serviu ao portão e aos criativos; a duração real da run (H4) só se mede com gente. **Reaproveitar:** DC `client/Assets/_DC/Scripts/Core/Bot.cs` (heurístico, com `Aggression`, `Greed` = apetite de risco e `Reaction` = handicap humano); Forge `client/tools/econsim/` (perfis × partidas → CSV).
- **Catálogo de exploits do §28 como testes nomeados**, um por linha: fechar o app antes de morrer, rewarded repetido, farm no 1º bloco, relógio para trás, semente repetida e save antigo ou futuro. No DC, a §28 virou teste do mesmo jeito.
- **Diário CSV de playtest.** **O que fazer:** gravar os eventos do §14 e os de 2026-10-09 (`plate_*`, `heat_level`, `extraction_*`), sem dado pessoal. O relatório calcula a H2 (concentração > 60% num ponto), a H3 (< 40% das placas recolhidas) e a H4. **Reaproveitar:** DC `client/Assets/_DC/Scripts/View/Exportar.cs` e `client/tools/diario_report.py`.
- **Flags de teste no build, todas sob `-testsession`.** **O que fazer:** `-tela`, `-arena A`, `-bloco N`, `-placas N` (mech cheio para foto e para o criativo #9), `-modulos a,b,c`, `-seed CÓDIGO`, `-boss`, `-bot`, `-lang`, `-shot`, `-record`, `-tutorial` e `-dev-desbloqueia`. **Por quê:** os criativos #1, #11 e #12 do §17 pedem exatamente esses estados, gravados do jogo real. **Reaproveitar:** DC `client/Assets/_DC/Scripts/View/Game.cs`.
- **Portão antes de todo PR.** **O que fazer:** seguir o `CONTRIBUTING.md` e somar `-autoplay 30` com 0 exceções e as fotos. Rodar o EditMode antes do PR, porque o NUnit do dotnet (3.14) e o do Unity (3.5) divergem. **Reaproveitar:** Forge `client/tools/verify.sh` e `client/tools/mutantes/mutantes.py`.
- **Textos em 4 idiomas e áudio sintetizado.** **O que fazer:** `L(pt, en, es, id)` com a frase inteira; os 9 sons do §12 gerados por script, com variações do auto-fire, que é o som mais repetido. **Reaproveitar:** DC `client/Assets/_DC/Scripts/View/Textos.cs` e `client/tools/audio_gen.py`. Armadilhas com solução pronta no DC: não ler PlayerPrefs em inicializador de campo, e usar `using Rect = UnityEngine.Rect;`.

### Arte e animação
**Decisão antes do 1º crédito: sprites pré-renderizados (como no DC) ou 3D em tempo real.** O 3D deixa os soquetes triviais ("filhos sem rig", `COMPETITIVO.md` D1), mas 150 malhas com esqueleto ameaçam os 30 FPS da H5. Recomendo sprites para os inimigos e decidir o mech na bancada da H5 (§28). O resto desta subseção assume sprites, pelo `render_sprites.py` do DC.
- **Módulos e placas separados do mech (regra do Vinicius), e aqui ela é o próprio hook.** **O que fazer:** os 7 tipos do §2 são gerados à parte e presos ao osso no render. Escudo no `mixamorig:LeftForeArm`; arma frontal e serra no `mixamorig:RightHand`; trilho no `mixamorig:RightShoulder`; capacitor nas costas, no `mixamorig:Spine2`, como a mochila do ferreiro do Forge. O drone não se prende: é um prop que voa ao lado. Como 6 módulos dão 64 combinações, cada módulo vira uma camada com os mesmos clipes, quadros e direções do mech, composta na View. Isso é **adaptação nova** do `--attach`, que hoje renderiza item e personagem juntos. Placas: começar com um deslocamento fixo por direção (8 direções × 24 soquetes, tabela na View); se a placa "flutuar" no passo, passar a âncora por quadro no `meta.json`, como o `--hold` já faz com a mão. **Por quê:** quando o Tripo gera item e corpo juntos, funde os dois e o rig arrasta o item errado (o guarda v1 do DC foi descartado por isso). **Reaproveitar:** DC `client/tools/render_sprites.py` (`--attach item:Osso:pos:rot:escala`, `--hold`, 4/8 direções e espelho); Forge `client/tools/folha_mochila.py` (antes × depois do item preso ao `Spine2`).
- **Mech do jogador (1 chassi no MVP).** Caminho: imagem grátis (4 opções, escolhida pela leitura no ângulo do jogo) → Modelo HD (45) → Auto Rig humanoide Mixamo (20) se o mech for bípede e estiver em pose T. Clipes que já existem:
  - parado: Forge `03_FORGE_STREET/arte/mixamo/Idle.fbx` (Breathing Idle, janela 199–289) ou DC `arte/mixamo/_blender/GuardIdle.fbx` (postura firme, pé no chão, mais "máquina");
  - andar e correr: ARKANA `mixamo-loc-andar-frente.fbx` e `mixamo-loc-correr-frente.fbx`. O `render_sprites.py` tira o root motion e grava `stride_mps`, e os −1,5% de velocidade por placa são só passo mais lento, sem clipe novo;
  - esquiva: DC `arte/mixamo/_blender/Dash.fbx`;
  - golpe leve: DC `_blender/Hit.fbx`; golpe pesado (arranca 3 placas): ARKANA `mixamo-standing-react-large-from-front.fbx`;
  - queda na arena (§3, "o mech cai"): ARKANA `mixamo-pouso-da-queda.fbx` e `mixamo-standing-land-to-standing-idle.fbx`;
  - extração concluída: Forge `Cheering.fbx`; morte: DC `_blender/Collapse.fbx` (desmorona de bruços).
  - Se o mech não for bípede (esteira, pernas de aranha), usar o rig "Outro" do Tripo (20) e clipes por keyframe no Blender, como o dragão do DC (`client/tools/dragao_blender.py`).
- **Inimigos robôs (MVP: 4 tipos, 1 elite e 1 chefe), por papel, com clipes que já existem:**
  - corpo a corpo leve: ARKANA `mixamo-loc-correr-frente.fbx` + DC `_blender/Punch.fbx` (impacto no quadro 6 de 12) + `_blender/Hit.fbx`;
  - kamikaze: ARKANA `mixamo-loc-correr-frente.fbx` + DC `_blender/MagmaSplit.fbx` (cambaleia, encolhe e estoura);
  - granadeiro: ARKANA `mixamo-loc-correr-tras.fbx` (recua, como o kobold do DC) + DC `_blender/KoboldToss.fbx` (soltura no quadro 7 de 12);
  - atirador de braço-canhão: clipe novo no DC `client/tools/anim_blender.py`, a partir das poses do `_blender/NecroCast.fbx` (aponta à frente, disparo no quadro 10 de 12; 0 crédito). Os clipes de magia do ARKANA foram testados no DC e liam como feitiço;
  - pesado e elite: o conjunto do golem do DC inteiro, `arte/mixamo/golem/` (`Idle`, `Walk`, `Slam`, `Charge`, `Stun`) + `golem_fim/Dying.fbx` (`Collapse`);
  - chefe: DC `_blender/Roar.fbx` (abertura), `Slam.fbx`, `Charge.fbx`, `Stun.fbx` (janela de dano depois da investida), `ForemanSpin.fbx` (giro de 360° = ataque de serra) e `Collapse.fbx`;
  - drone inimigo: prop sem rig (45, ou primitivas no Blender a 0 crédito), com balanço e inclinação na View.
  - O "telegraph claro" do §3 sai do quadro de impacto, que já está medido para cada clipe na tabela do DC `docs/PROVENIENCIA.md` §3. O Core usa a mesma fração para a janela de esquiva. Nunca mover action crua entre esqueletos: o retarget é por delta de rotação sobre o repouso.
- **Elite e variantes por troca de cor, 0 crédito.** **O que fazer:** o elite é o inimigo comum recolorido e com `--escala 1.3`; o evento "Toxic Scrapstorm" (§9) é a paleta verde; as skins de chassi (cosmético) são o recolor da folha. **Reaproveitar:** DC `client/tools/roupas_cor.py` e `client/tools/roupas_2d.py` (direto na folha, com luz chapada).
- **Blender por script em vez de gerar de novo.** **O que fazer:** placas, capacitor, trilho, escudo e a cápsula de extração por primitivas, a 0 crédito; a cápsula que abre segue o corte com dobradiça do baú do DC. **Reaproveitar:** Forge `client/tools/props_blender.py` e `itens_blender.py`; DC `client/tools/bau_abrindo.py`.
- **Interface pintada no gerador grátis.** **O que fazer:** logo, ícones dos módulos para as cartas 1-de-3 (folha 4×3 sobre azul-marinho liso), fundo do hangar e retratos da operadora e do chefe. **Reaproveitar:** DC `client/tools/ui_assets.py`.
- **Nitidez × tamanho.** **O que fazer:** folha HD só para o mech e o chefe (`--hd K --escala E`, com K = min(1,5; 4096 / (quadros × célula))); inimigos comuns em resolução menor. **Por quê:** no DC, as folhas HD levaram o APK de 67,7 para 83 MiB. **Reaproveitar:** DC `client/tools/elenco_hd.sh`.
- **Custo estimado em créditos do Tripo (Lote 1, com aval):** mech 65 + 3 inimigos humanoides (3 × 65 = 195) + drone 45 + chefe 65 + arma frontal e serra, que não saem bem por primitivas (2 × 45 = 90) ≈ **460**, com teto de 550. Elite, variantes, placas, cápsula, demais módulos e UI custam 0. Referência: o Lote 1 do DC custou 530 (10 modelos + 4 rigs). Conferir o saldo antes e depois e a receita do painel na 1ª peça.

### Interface e marca
- **UI procedural em 9-fatias, tingida por código:** cartas de módulo (`Moldura`, `Botao`), anel de extração (`Contorno`), barra de calor e números de sucata com `Letreiro`. **Reaproveitar:** DC `client/Assets/_DC/Scripts/View/Art.cs`. Fontes OFL: Lilita One e Nunito ExtraBold, com a licença junto.
- **Escala e toque.** CanvasScaler 1080×1920 casando a largura, `AreaSegura` e `Dp` (48 dp). **Reaproveitar:** DC `client/Assets/_DC/Scripts/View/AreaSegura.cs` e `Dp.cs`, as mesmas classes que o §13 cita no ARKANA.
- **Telas 20:9.** **O que fazer:** a arena continua escurecida até a borda; a tempestade é o fundo natural fora da área de jogo. **Por quê:** no DC, faixa lisa na borda parecia bug.
- **Ícone adaptativo:** o mech com placas, ocupando no máximo 0,64 da camada, conferido nas máscaras círculo, squircle e quadrado (DC `client/tools/icone_app.py`). O retrato do cartão de ferro-velho (D5) sai do recorte do quadro (`SpriteSheet.Retrato` em DC `client/Assets/_DC/Scripts/View/SpriteSheet.cs`).

### Onboarding (tutorial guiado)
Tour do DC: a Sim congela nos passos de explicação (no passo fixo é trivial, e ninguém toma dano lendo), véu com buraco, contorno dourado, seta e cartão com o que é, quando usar e por quê. Nos passos de ação, só o alvo responde. Cada passo aparece uma vez, com "Pular tutorial" e "REVER TUTORIAL", desligado no `-testsession`. Passo de ação se cancela se a tela mudar (no DC, um passo preso congelou o jogo depois do resultado). **Reaproveitar:** DC `client/Assets/_DC/Scripts/View/Tour.cs` (troca só os passos e os gatilhos).

| # | Quando (gatilho) | O que acende | Cartão: o que · por quê |
|---|---|---|---|
| 0 | run 1, antes do 1º toque | cartão da operadora (abaixo) | quem manda o mech e o que pede |
| 1 | run 1, mech pousado | a tela toda (ação: andar 1,5 m) | "Arraste o dedo para andar" · o verbo central vem antes de qualquer escolha |
| 2 | 1º inimigo no alcance | o inimigo e o tiro | "O mech atira sozinho no mais perto; você cuida de onde ficar" |
| 3 | 1ª sucata recolhida | a placa nova no corpo | "Sucata vira blindagem: segura golpes, pesa e atrai robôs" · é o hook D1 no 1º minuto |
| 4 | 1º marco de XP | as 3 cartas (ação: escolher) | "Escolha 1. Ele se prende ao mech até o fim da run" |
| 5 | 1º golpe forte (~2:00) | as placas no chão (ação: recolher 1 em 3 s) | "Placas caíram! Passe por cima antes que sumam" · a H3 depende disso |
| 6 | 1º ataque com telegraph | o aviso no chão (ação: esquivar) | "Toque rápido = esquiva" |
| 7 | tempestade fechando | seta para a cápsula | "A tempestade está fechando. Vá até a cápsula" |
| 8 | dentro do círculo | anel de 5 s e barra de calor | "Fique 5 s. Mais placas = mais robôs vindo" |
| 9 | hangar, 1ª vez | saldo de sucata e 1º sidegrade (ação: comprar) | "Isto é o que você salvou. Compre a 1ª melhoria" · o valor da sucata vem antes do risco |
| 10 | run 2, 1º fim de bloco | a cápsula e o "x1,5" do bloco 2 | "Extrair com o que tem ou seguir por x1,5?" · a 1ª escolha real |
| 11 | 1ª vez com calor > 75% | o contorno pulsante | "Calor alto: a horda engrossa" |

- **Cartão de contexto em vez de cutscene.** **O que fazer:** a queda do mech (§3) é o 1º plano de jogo, sem cena antes. No lugar do 1º cartão do tour entra um retrato pintado de quem manda o mech, com balão de fala. Exemplo (PROPOSTO; o GDD ainda não tem personagem nomeado), a operadora do ferro-velho: *"Tempestade chegando. Junta toda sucata que der e volta inteiro: a cápsula desce quando o céu fechar."*. O ciclo fecha no hangar, com a fala dela sobre o que voltou. **Por quê:** no DC, a cutscene antes do 1º toque somava com o tutorial e virava parede de texto.
- **Controle sem desenho tampando o mech e as placas.** **O que fazer:** o joystick do §2 fica invisível por padrão (mesma lógica, sem desenho sob o dedo), com a opção "Controle na tela" nas configurações. A dodge é o toque rápido, como o dash do DC. **Por quê:** no DC, o joystick desenhado tampava o personagem. Aqui ele tamparia também as placas caídas que o jogador tem 3 s para recolher. O gênero costuma mostrar o joystick; se a Camada 0 pedir, ligar o desenho pequeno e translúcido. **Reaproveitar:** DC `client/Assets/_DC/Scripts/View/Joystick.cs` (`JoystickLogica` pura, que veio do ARKANA via Forge Street, e `Joystick.Visivel`).

### Monetização e compliance
- **Dentro dos guardrails, conferido:** 1 moeda (Sucata), Cores e Blueprints fora do MVP (§6); sem energia; caixa do dia com conteúdo visível; interstitial desligado na v0.1; rewarded opcional com id de transação `rw-<runId>-<tipo>` (§7); "sem energia, sem gacha" como posicionamento (D4).
- **Anúncio não personalizado para todos e sem `AD_ID` (falta no GDD).** O público do §1 começa em 13 anos, então isso não é opcional aqui. **O que fazer:** `LevelPlayPrivacySettings` antes do `Init` (GDPR sem consentimento, CCPA opt-out, COPPA desligado), o manifesto sem `AD_ID` e sem as permissões do Privacy Sandbox, e "não" na declaração de ID de publicidade. **Reaproveitar:** DC `client/Assets/_DC/Scripts/View/Anuncios.cs`, `AnunciosLevelPlay.cs`, a classe `SemIdDePublicidade` em `client/Assets/_DC/Editor/Setup.cs` e `docs/MONETIZACAO.md` §4.
- **IAP.** Remove Ads e Starter Pack de conteúdo fixo, com compra em 2 passos, loja falsa no PC e "Restaurar compras". **Reaproveitar:** DC `client/Assets/_DC/Scripts/View/Loja.cs` e `LojaIap.cs`.
- **Política de privacidade** no GitHub Pages, em 4 idiomas, citando as redes usadas (modelo: https://vvs2705.github.io/dungeon-courier/).

### Play e lançamento
- **Conta da Play: a de organização da V-STACK, uma só para todos os jogos.** O D-U-N-S já foi pedido pelo DC (previsão 2026-11-25); o Scrapstorm entra na mesma conta. O appId `br.com.vstack.scrapstorm` é fixado no `Setup.cs` e não muda depois do 1º upload. Conferir a marca "Scrapstorm" antes da loja.
- **Chave de upload própria** em `%USERPROFILE%/.scrapstorm/`, fora do git e com backup fora do PC.
- **AAB assinado por `Setup.BuildAndroidBundle`** (no DC, foram conferidos targetSdk 36, 16 KB e Billing 9).
- **Loja e criativos pelos scripts, só com gameplay real:** DC `client/tools/loja_fotos.sh`, `loja_assets.py` e `criativos.py`. O cartão final "sem energia, sem gacha" (#13 do §17) entra no CTA do `criativos.py`. Pré-release no GitHub a cada versão.

### Android
- **`vSyncCount = 0` e `targetFrameRate = 60` no início** (no DC, o POCO foi de 28–36 para 55 fps). Com horda, medir antes de prometer 60: o piso do §26 é 30.
- **Desempenho e calor se medem em aparelho original de entrada, não no POCO do Vinicius**, que se limita depois de 1 min e não serve de régua para a H5. **Reaproveitar:** Forge `client/tools/medir_aparelho.sh` (FPS do SurfaceFlinger, memória, `--temp-serie 30` para a temperatura numa sessão longa) e a `BancadaDeCortes`/`MedidorDeFps` do ARKANA (§13).
- **APK de worktree via `subst R: <client>`**, só o APK atual e o adb com aspas internas nos argumentos (`-e unity '-bot -seed X'`).

### Conflitos com o GDD atual
Esta seção só aponta os conflitos; as seções acima no GDD não foram editadas.

| Onde | O que o GDD diz | Lição contrariada | Recomendação |
|---|---|---|---|
| README e `COMPETITIVO.md` (e) | lote de criativos "antes de qualquer código" | regra do estúdio: criativo só de gameplay real | antes do lote, fazer o greybox mínimo (núcleo + bot + `-record`, arte de 0 crédito por primitivas e pintura grátis) e gravar os criativos dele. Mockup sem jogo não entra |
| §2 Core mechanic | "joystick virtual de um dedo" | controle sem desenho tampando o personagem | invisível por padrão, com a opção nas configurações; conferir em foto se o dedo esconde as placas caídas |
| §3 (roteiro original, 9:00–10:00) | "primeira reward chest" | nada aleatório | baú do hangar com conteúdo visível antes de abrir, como a revisão do §7 já faz com a caixa do dia |
| §6 tabela e §7 Rewarded | reroll de módulo (1 grátis; os demais por rewarded) | nada aleatório pago, nem por moeda | ok só por rewarded; nunca por IAP nem por sucata. Se o Starter Pack trouxer sucata, o reroll não pode custar sucata |
| §7 IAP (lista original) | "cores" e "event pack" | 1 moeda; conteúdo fixo | já adiado para a v1.0; manter Cores fora até existir mapa de fontes e ralos, e pacote sempre com conteúdo listado |
| §13 e §23 | joystick do ARKANA "a desacoplar"; `AreaSegura`, `Dp` do ARKANA | copiar o que já foi pago | pegar a versão do DC: `JoystickLogica` já desacoplada em `Joystick.cs`, mais `AreaSegura.cs` e `Dp.cs` |
| §11 | "módulos encaixáveis fisicamente", sem regra de produção | itens gerados separados do corpo | módulos e placas nunca no mesmo modelo do mech; render em camadas (subseção Arte) |
| §26 e §28 H5 | "30 FPS de piso nos aparelhos-alvo mínimos" | desempenho se mede em aparelho original | definir já qual aparelho de entrada é a régua; o POCO F4 não serve |

### Primeiros passos recomendados
O Scrapstorm está na fila como "depois" (README). Os passos 1 e 2 cabem antes da vez dele; o resto só quando o Vinicius liberar.
1. Resolver os conflitos acima no GDD (reroll, baú, joystick, ordem greybox → criativos) e escolher o aparelho de entrada da H5.
2. Escrever `docs/CONTRATO_V01.md` e criar a memória `STATUS_scrapstorm-v01.md`.
3. Copiar o esqueleto do DC e fazer o núcleo em passo fixo com semente, com `Joystick.cs` e os exploits do §28 como testes nomeados.
4. Bot com 3 políticas de extração e `-autoplay`: provar a H2 no bot antes de gastar arte.
5. Bancada de 150 inimigos + 24 placas no aparelho de entrada (`medir_aparelho.sh`), para decidir sprite × 3D (H5).
6. Greybox com arte de 0 crédito e `-record`; gravar o lote de 8–10 criativos (H1) com o cartão "sem energia, sem gacha".
7. Se a H1 passar: Lote 1 do Tripo (~460 créditos, com aval) e os clipes reaproveitados da lista acima.
8. Tour com os 12 passos acima, cartão da operadora, diário CSV e Camada 0 com 5–8 pessoas (H2, H3).
