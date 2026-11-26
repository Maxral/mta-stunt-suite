# Manual Completo — Stunt System + Stunt Tools (v1.0.0)

[English version](MANUAL_COMPLETO_EN.md) · [README](../README.md)

## Índice

1. [Visão geral](#1-visão-geral)
2. [Instalação e ACL](#2-instalação-e-acl)
3. [Temas, idiomas e fonte](#3-temas-idiomas-e-fonte)
4. [stunt_tools — Hub F7](#4-stunt_tools--hub-f7)
5. [Saves e Warps](#5-saves-e-warps)
6. [Atalhos e ferramentas de treino](#6-atalhos-e-ferramentas-de-treino)
7. [Modo Espectador](#7-modo-espectador)
8. [Replay segmentado / TAS](#8-replay-segmentado--tas)
9. [Galeria de Replays e Player](#9-galeria-de-replays-e-player)
10. [Modo Ghost, rastro 3D e loop A-B](#10-modo-ghost-rastro-3d-e-loop-a-b)
11. [Editor de corte](#11-editor-de-corte)
12. [Painel Admin: /configwarp](#12-painel-admin-configwarp)
13. [stunt_system — Gerenciador da Arena](#13-stunt_system--gerenciador-da-arena)
14. [Configurações & Dificuldades](#14-configurações--dificuldades)
15. [Observações nos stunts](#15-observações-nos-stunts)
16. [Mapa F2, radar e CV Zones](#16-mapa-f2-radar-e-cv-zones)
17. [Comandos — referência](#17-comandos--referência)
18. [Auto-Update](#18-auto-update)
19. [Arquivos de dados e backups](#19-arquivos-de-dados-e-backups)
20. [Solução de problemas](#20-solução-de-problemas)

---

## 1. Visão geral

- **`stunt_system`** cuida da *arena*: carrega os stunts do mapa, registra conclusões, recordes e ranking, desenha o mapa F2 e oferece o Gerenciador da Arena.
- **`stunt_tools`** cuida do *treino e da criação*: saves/warps, gravação e reprodução de replays, Modo Ghost, freecam e utilidades.

Cada resource funciona sozinho. Quando os dois rodam, **idioma, tema e fonte são sincronizados** nos dois sentidos.

## 2. Instalação e ACL

Veja o [README](../README.md#installation). Resumo:

- Pastas em `resources/`, `refresh`, `start stunt_system`, `start stunt_tools`.
- Conta de Admin no grupo ACL **Admin**.
- Resources com `function.fetchRemote` (e `function.restartResource`) para o auto-update.
- **Desative outros scripts de Freecam/CamHack que usem `H`.**

## 3. Temas, idiomas e fonte

- **Idiomas:** seletor `PT | EN` no canto esquerdo do cabeçalho dos menus. **O padrão na primeira entrada é Inglês (EN)**; a escolha manual fica salva e vale para os dois resources. Novos idiomas: copie `lang/en.xml` para `lang/xx.xml`.
- **Temas** (F7 → Configurações → TEMA, ou botão TEMA em Configurações & Dificuldades; vale para os dois resources):
  | Tema | Aparência |
  |---|---|
  | **Híbrido** (padrão) | Visual do Moderno com layout compacto e ícones vetoriais do Minimalista. |
  | **Moderno** | Painéis Dark Glass com laranja de destaque. |
  | **Minimalista** | Barras compactas, botões-ícone com tooltip, switches deslizantes. |
  | **Clássico** | Controles nativos do MTA com o skin básico. |
- **Fonte:** Padrão → Segoe UI → Bahnschrift → Calibri (Configurações → FONTE).
- **Selo de versão:** no rodapé dos dois menus aparece `v1.0.0` em cinza discreto, lido do `meta.xml`. Para Admins, com versão nova no GitHub, vira `v1.0.0 • Nova versão disponível` em laranja.

## 4. stunt_tools — Hub F7

Abra com **F7** (fecha todas as janelas do hub se já houver alguma aberta).

- **Lista de jogadores** com ID, nome, veículo e **Status** (AFK, em replay, etc.).
- Botões: **TELEPORTAR** (warp para o save do jogador selecionado), **COPIAR SAVE**, **ASSISTIR (WATCH)**, **AJUDA**, **CONFIGURAR TECLAS** (Configurações), **REPLAYS** (Galeria), **MEU WARP: PRIVADO**, **COMANDO /CV**.
- **Engrenagem ADM** (só Admin): abre o painel `/configwarp`.
- Rodapé: descrição do botão sob o mouse, versão e créditos.

### Configurações (CONFIGURAR TECLAS)

Teclas padrão (todas reatribuíveis; `Backspace` remove a tecla; APLICAR E SALVAR grava):

| Ação | Tecla | Ação | Tecla |
|---|---|---|---|
| Salvar (`/sw`) | `1` | Gravar Replay | `F10` |
| Voltar (`/lw`) | `2` | Parar Ghost | `L` |
| Deletar (`/dw`) | `3` | Abrir Galeria | `F4` |
| Privado | `4` | Freecam + Teleporte | `H` |
| Auto-Tap Moto | `Shift esq.` | Reparar / Desvirar | `R` |
| Objetos Invisíveis | `I` | Instalar / Recarregar Nitro | `N` |
| Ocultar Jogadores | `O` | Ligar / Desligar Motor | `J` |
| Jogadores Transparentes | `K` | | |

Opções que valem na hora (salvas automaticamente): **Modo do Auto-Tap** (segurar/alternar), **HUD Velocímetro**, **Reajuste de câmera no /lw**, **RASTRO 3D DO GHOST** (ON/OFF, padrão ON), **TEMA**, **FONTE**, **RESTAURAR PADRÕES**.

## 5. Saves e Warps

| Comando | Tecla | Função |
|---|---|---|
| `/save` ou `/sw` | `1` | Salva posição, rotação, velocidade e veículo |
| `/warp` ou `/lw` | `2` | Volta ao último save |
| `/delwarp` ou `/dw` | `3` | Apaga o último save |
| `/sw 1` … `/sw 5` / `/lw 1` … `/lw 5` | — | **Slots fixos de treino** (precisa de login; persistem na conta) |
| `/privado` | `4` | Alterna MEU WARP privado (outros não podem copiar/teleportar) |
| `/copiarsave` / `/cwarp` | — | Copia o save de quem você assiste (ou `[id/nome]`) |

No **Modo Play** (dimensão 0) o `/sw` só salva com o veículo parado (até 5 km/h) e no chão; a equipe (Admin / SuperModerator / Moderator) salva livremente. O histórico guarda até 20 saves por jogador (configurável).

## 6. Atalhos e ferramentas de treino

- `/cv [nome ou ID]`, `/v` — spawn de veículo (respeita a CV Zone no modo Gamemode); `/del` — remove o seu veículo; `/gm` ou `/ghostmode` — liga/desliga a **colisão com outros jogadores e veículos** (padrão: ligado = sem colisão, "ghostmode").
- `/timeset [hora]` (ex.: `17:30`) e `/w [id]` — hora e clima **só no seu jogo**; o relógio fica congelado em 12:00 por padrão.
- `/stanthud` ou `/stunthud` — HUD velocímetro (KM/H, MPH, marcha/RPM, nitro). Padrão desligado.
- **`I`** Objetos Invisíveis · **`O`** Ocultar Jogadores · **`K`** Jogadores Transparentes (`O` e `K` se substituem).
- **`H`** Freecam + Teleporte · **`R`** reparar/desvirar · **`N`** nitro · **`J`** motor.
- `/objdebug` — diagnóstico de como o mapa esconde os objetos (alpha, escala, dimensão); `/fixdim [id ou nome]` — **só equipe**: encerra watch/replay do jogador e leva ele e o veículo para a dimensão 200 (editor) ou 0 (Play).

## 7. Modo Espectador

`/watch [id ou nome]` ou o botão **ASSISTIR** do F7. A câmera segue o jogador; você fica guardado (congelado, invisível, sem colisão). `Backspace` ou `/watch` sai e devolve você ao mesmo ponto e veículo. Respeita o MEU WARP PRIVADO. No Modo Play é preciso estar parado e no chão para começar.

## 8. Replay segmentado / TAS

- **`F10`** começa a gravar seus inputs. Cada **save (`/sw`)** vira um checkpoint e cada **warp (`/lw`)** apaga a tentativa errada e rebobina a gravação até o save, então **sobra só a run limpa**.
- `F10` de novo finaliza: nomeie e escolha **SALVAR LOCAL (.CSV)**, **SALVAR E PUBLICAR NA GALERIA** ou **DESCARTAR**.
- Dá para **continuar uma gravação** de um replay (CONTINUAR DAQUI / CONTINUAR GRAVAÇÃO), **clonar para rascunho** e **juntar replays**.
- `/gravarstunt <id>` ou `/gravarstunt l<índice>` — abre um replay (publicado pelo id, ou da lista local pelo índice) no player em modo de gravação/fila (Modo Cinema).

## 9. Galeria de Replays e Player

Abra com **F4**, `/replays` ou o botão REPLAYS do F7.

- Abas: **Todos**, **Meus Replays (local)**, **Galeria Geral**, **Rascunhos**, **Publicados**; filtros por criador e ordenação (recentes, antigos, maior/menor duração, nome); busca por nome/criador/veículo.
- Ações: **ASSISTIR** (duplo clique), **CONTINUAR**, **CLONAR**, **JUNTAR**, **PUBLICAR**, **RENOMEAR**, **EXPORTAR .CSV**, **DELETAR** (com confirmação), copiar pasta.
- **Player:** `Espaço` play/pause · `←/→` −3 s/+3 s · clique na barra para pular · velocidades 0.1x–4x · **LOOP** · `K` câmera **FOLLOW/FLYCAM** · `H` oculta a interface · `Esc`/`Backspace` sai.
  - **FOLLOW:** câmera do GTA seguindo o carro (`V` muda a distância).
  - **FLYCAM:** `WASD` move, `Q/E` desce/sobe, `Shift` rápido, `Ctrl` lento, scroll muda a velocidade.
  - Aplica hora e clima da gravação e devolve os seus ao sair. Losangos na linha do tempo marcam os saves.
- **Loop A-B:** tecla **L** (ou botão **A-B**): 1º clique marca **A**, 2º marca **B** e liga o loop, 3º limpa.
- **Playlist:** `|<` anterior / próximo `>|` conforme a lista de onde você clicou ASSISTIR; **Modo Cinema** (fila) para gravar sequências.

## 10. Modo Ghost, rastro 3D e loop A-B

Na Galeria, escolha o modo e clique em **CORRER CONTRA (GHOST)**. Você continua dirigindo e um carro translúcido, sem colisão e mudo, refaz a run.

| Modo | Comportamento |
|---|---|
| **Sync com Warp + Loop** | Ao ativar, o servidor te coloca na largada com auto-save; o ghost espera você acelerar e **larga junto com você a cada `/lw`**. |
| **Apenas Loop Contínuo** | O ghost roda sem parar, ignorando warps. |
| **Gravar Fila (Modo Cinema)** | Playlist contínua para gravar. |

**Rastro 3D (`RASTRO 3D DO GHOST`):** uma linha 3D contínua mostra a trajetória exata do ghost, no chão e no ar, com degradê da cauda (ciano, transparente) à cabeça (laranja, opaca). É limpo a cada reinício do loop, sem linhas cruzando o mapa. **ON/OFF**, padrão **ON**, na linha do Ghost da Galeria e em **F7 → Configurações**; a escolha é salva.

**Trecho A-B:** marque **A** e **B** no player, saia dele e ative o Ghost **do mesmo replay**. O ghost roda em loop **apenas dentro de A–B**: começa exatamente em A e reinicia em A ao chegar em B; o modo Sync também larga do A. Sem A-B, ele usa a largada automática e vai até o fim. O card inferior mostra `A-B 00:05 → 00:09` e o progresso do trecho. O A-B vale enquanto o jogo estiver aberto.

Para parar: **`L`**, `/stopghost` ou **PARAR GHOST**.

## 11. Editor de corte

No player, o botão de **tesoura** abre o editor sobre a linha do tempo: arraste **[ INÍCIO** e **FIM ]** para aparar as pontas e use **+ TRECHO** para criar trechos a remover (alças arrastáveis; clique direito remove). **APLICAR CORTE** salva uma **cópia `_cut`**; o original permanece intacto.

## 12. Painel Admin: /configwarp

Só Admin (engrenagem **ADM** no F7 ou `/configwarp`). Alterações valem ao vivo para todos e são gravadas em `config_warp.json`:

| Opção | Padrão | Efeito |
|---|---|---|
| Assentamento (ms) | 400 | Tempo congelado no ponto antes de soltar o `/lw` (0–1500) |
| Salvar velocidade | ON | `/lw` restaura velocidades linear/angular |
| Cooldown do `/lw` (s) | 0 | Intervalo entre dois `/lw` (0–10) |
| Permitir copiar | ON | Botão COPIAR SAVE, `/copiarsave`, `/cwarp` |
| Máx. de saves | 20 | Histórico por jogador (1–50) |
| Permitir salvar no ar | ON | `/sw` em queda |
| Reparar no `/lw` | ON | Conserta o veículo ao voltar |
| Editor volta ao ponto | ON | F6 do Map Editor: ON = ao sair da edição você volta ao ponto de antes de editar; OFF = vai para onde a câmera do editor estava |

**SALVAR CONFIGURAÇÕES** grava; **RESTAURAR PADRÕES** volta tudo.

## 13. stunt_system — Gerenciador da Arena

Abra com **`Alt+F2`** ou `/stunts` (fechar: mesma tecla).

- Lista de stunts da **arena ativa** (marcada com `[STUNTAGE]` no mapa) com nome, veículo, valor, dificuldade (cor do nome) e tipo (touch, 3s, challenge). Barra de filtros: **Pesquisar**, **Tipo** (Touch / 3s / Challenge), **Status** (Em Teste / Testados), **Dificuldade**, **Progresso** (Pendentes / Completos), **Ordenar por** e **Limpar**. Barra de resumo: arena, total, testados e em teste.
- **Duplo clique** (ou `Enter`) teleporta ao stunt selecionado — só para a **equipe** (grupos ACL Admin / SuperModerator / Moderator, quem tem o direito `resource.stunt_system.manage` ou a permissão `command.kick`). Rodapé: `Exibindo N de M stunts`.
- Botões: **SINCRONIZAR MAPA** (recarrega os stunts do arquivo do mapa, com confirmação), **TESTADO / EM TESTE** (equipe), **MARKERS TESTADOS** (mostra/oculta em roxo), **MARCAR PENDENTE** (volta seu progresso do stunt), **CONFIGURAÇÕES**.
- Idiomas e selo de versão no cabeçalho/rodapé.

## 14. Configurações & Dificuldades

Painel lateral do Gerenciador:

- **Faixas de dificuldade:** tetos em `$` (crescentes; *Demonic* = acima do teto de *Very Hard*). Só a **equipe** (mesmo critério acima) altera; ao salvar, todos os jogadores online são atualizados.
- **Modo do resource (só Admin):** **GAMEMODE COMPLETO** (dinheiro real, saldo na conta, RANKING no F2, spawn nos peds e CV Zone no `/cv`) ou **CRIADOR (PLUGIN)** (só ferramentas de criação, sem dinheiro/ranking/spawn forçado/bloqueio do `/cv`).
- **TEMA** e **FONTE** (valem para o stunt_tools).
- **RESETAR MEU PROGRESSO:** apaga só os seus stunts completos na arena atual.

## 15. Observações nos stunts

Clique com o **botão direito** num stunt da lista para abrir o menu **Adicionar / Editar / Remover Observação**. Só a **equipe** edita; o texto é limpo (sem quebras de linha nem códigos `#RRGGBB`) e limitado a **100 caracteres**. A observação fica salva por arena e aparece em laranja/branco logo abaixo do stunt selecionado, para todos os jogadores.

## 16. Mapa F2, radar e CV Zones

- **`F2`** abre/fecha o mapa customizado da arena (`F11` = mapa nativo). Scroll = zoom; arraste = mover. Gavetas **VEÍCULOS**, **STUNTS** (busca; duplo clique teleporta — equipe) e **RANKING** (Top Stunters e Top Recordistas; só no modo Gamemode).
- Ícone azul **CV**: teleporta ao Spawn Point da CV Zone.
- Seta do jogador no mapa e no radar.
- **CV Zones:** peds de spawn + cilindro verde configurados nas arenas `[STUNTAGE]`.

## 17. Comandos — referência

**stunt_system:** `/stunts` (abre/fecha o Gerenciador), `/blips` (recria as blips), `/blipsize [1-25]` (tamanho das blips), `/mvs` ou `/markvehiclestunts` (filtro de stunts por veículo no radar/F11), `/mark` (rastreia um jogador no radar/F11), `/resetstunts` (recria markers e blips e recarrega o estado do servidor — **não** apaga progresso), `/resetstunt [nome]` (zera o **seu** progresso naquele stunt; com `all` no fim, **só Admin**, zera para todos), `/resetallstunts` (zera todos os **seus** stunts da arena ativa), `/stuntarena` (mostra a arena ativa; equipe: `/stuntarena [nome]` força o nome, `/stuntarena off` volta à detecção automática), `/stuntdiag [nome]` (equipe: diagnóstico das cópias de um stunt), `/cvdiag` (diagnóstico do bloqueio do `/cv` para você), **`/atualizarstunt`** (Admin).

**stunt_tools:** `/sw` `/save` · `/lw` `/warp` · `/dw` `/delwarp` · `/privado` · `/copiarsave` `/cwarp` · `/watch` · `/cv` `/v` · `/del` · `/gm` `/ghostmode` · `/timeset` · `/w` · `/stanthud` `/stunthud` · `/replays` · `/stopghost` · `/gravarstunt` · `/replaysync [arquivo.csv]` (equipe: sincroniza a pasta `replays_publicos/` ou importa um arquivo) · `/configwarp` (Admin) · `/objdebug` · `/fixdim` (equipe) · **`/atualizartools`** (Admin).

## 18. Auto-Update

Detalhes no [README](../README.md#auto-update). Em resumo: verificação 5 s após iniciar e a cada 6 h via `fetchRemote`; aviso no console e para Admins no chat (com changelog e instrução); `/atualizarstunt` e `/atualizartools` baixam os arquivos do `version.json`, fazem **backup em `_backup_update/`**, substituem e reiniciam o resource. Erros de rede/ACL são silenciosos (uma linha no console).

## 19. Arquivos de dados e backups

Nunca sobrescritos pelo updater: `stunts.db`, `saves_stunt.db`, `replays.db`, `config_warp.json`, `replays_publicos/`, `replays/`, `saves/`. Preferências do jogador ficam no **cliente** (`binds.xml`, `hub_lang.xml`/`stunt_lang.xml`, `fonte_pref.xml`). Backups de updates: `<resource>/_backup_update/<timestamp>_v<versão>/` — para voltar, copie os arquivos de volta e dê `/restart`.

## 20. Solução de problemas

| Sintoma | Causa provável / solução |
|---|---|
| Console: *Auto-update disabled* | Falta `function.fetchRemote` na ACL dos resources. |
| `/atualizar…` diz que não consegue consultar o GitHub | Sem internet, GitHub fora ou URL do `manifesto` ainda com `Maxral/mta-stunt-suite`. |
| `H` não abre a freecam | Outro resource usa `H`; desative-o ou troque a tecla. |
| Ghost não usa o A-B | O A-B precisa ser marcado no player **do mesmo replay** e o player fechado antes de ativar o Ghost. |
| Selo "Nova versão" não aparece | Só Admins (ACL) recebem o aviso; confira o grupo e a checagem de 6 h. |
| Idioma inicial em inglês | É o padrão; troque no seletor `PT / EN` (fica salvo). |
