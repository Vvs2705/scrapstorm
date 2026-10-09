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
