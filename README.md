# Scrapstorm

**Estilo:** survivor-like de ação casual com um mech, controle de um dedo, retrato.

**O que é:** partidas curtas de sobrevivência pilotando um mech feito de sucata.

**Como funciona:** você move o mech com um dedo e ele atira sozinho; ondas de robôs deixam XP e sucata. A sucata vira placas de blindagem no corpo do mech (o golpe arranca, dá para recolher). A cada marco você escolhe 1 de 3 módulos e o mech muda de aparência. A tempestade marca o tempo: ao fim de cada bloco você decide se extrai (exposto por alguns segundos) ou arrisca seguir.

**Como vai ser jogar:** montar uma build diferente a cada partida e decidir até onde arriscar; no hangar, as melhorias ficam.

## Situação
Depois (os ganchos "monte seu mech" e "extraia ou arrisque" já têm donos no mercado; validar por criativos antes de código). Ainda não há código: este repositório guarda o GDD e a estrutura do projeto, pronta para o desenvolvimento começar.

- **GDD:** [`docs/GDD.md`](docs/GDD.md) (revisão competitiva de 2026-10-09 no topo).
- **Comparativo com jogos similares e diferenciais:** [`docs/COMPETITIVO.md`](docs/COMPETITIVO.md).

## Estrutura do repositório
| Pasta | Para quê |
|---|---|
| `docs/` | GDD, comparativo e, depois, balance, validações e contratos de cada fase |
| `client/` | projeto Unity 6 (6000.3.x), Android primeiro, retrato; código do jogo em `client/Assets/_SS/` |
| `client/Assets/_SS/Scripts/Core/` | núcleo em C# puro (regras, simulação, save), testável fora do Unity |
| `client/Assets/_SS/Scripts/View/` | MonoBehaviours, UI, câmera, entrada |
| `client/Assets/_SS/Editor/` | setup do projeto e builds por linha de comando |
| `client/Assets/_SS/Tests/EditMode/` | testes NUnit do núcleo |
| `client/Assets/_SS/Resources/` | sprites e dados carregados em tempo de execução |
| `client/tools/` | ferramentas fora do Unity (testes `dotnet`, scripts de arte, relatório de playtest) |
| `arte/` | arte-fonte; `arte/tripo/` e `arte/mixamo/` ficam fora do git |

Como contribuir: [`CONTRIBUTING.md`](CONTRIBUTING.md). Histórico: [`CHANGELOG.md`](CHANGELOG.md).

## Repositório e licença
© V-STACK / Vinicius Souza. **Todos os direitos reservados.** Código, documentos e arte visíveis para acompanhamento, sem licença de uso, cópia ou redistribuição.
