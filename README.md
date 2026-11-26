# Stunt System + Stunt Tools

**EN** · [Português](#português)

Two companion MTA:SA resources for stunt servers and stunt creators:

| Resource | What it is |
|---|---|
| **`stunt_system`** | Stunt arena engine: markers, completion/records/ranking, custom F2 map, Arena Manager (`Alt+F2` / `/stunts`), difficulty settings, stunt notes, CV zones. |
| **`stunt_tools`** | Training and creation hub: saves/warps (`/sw` `/lw` `/dw`), F7 Hub, Replay / TAS recorder, Replay Gallery, Ghost mode with 3D trail and A-B loop, cut editor, freecam, speedometer HUD. |

They work alone, but share language, theme and font preferences when both run (`PT` / `EN` selector, themes *Hybrid*, *Modern*, *Minimalist*, *Classic*). Current version: **v1.0.0**.

## Installation

1. Copy the `stunt_system` and `stunt_tools` folders to `server/mods/deathmatch/resources/`.
2. Edit `server/mods/deathmatch/acl.xml` (see below), then restart the server (or `aclreload`).
3. In the console: `refresh`, then `start stunt_system` and `start stunt_tools`.
4. Add both to `mtaserver.conf` (`<resource src="stunt_system" startup="1" protected="0" />`) to start automatically.

> **Disable other scripts that bind `H` to Freecam / CamHack.** `stunt_tools` ships its own freecam + teleport on `H` (plus `R` repair, `N` nitro, `J` engine). Two resources using the same key will conflict. Keys can be changed in **F7 → Settings**.

## Required `acl.xml` setup

Admin features (update commands, `/configwarp`, difficulty editing, mode switch) require the account to be in the ACL group **Admin**:

```xml
<group name="Admin">
    <acl name="Admin"></acl>
    <object name="user.YourAccountName"></object>
</group>
```

For the auto-update check the **resources** need permission to call `fetchRemote` (and `restartResource` to restart themselves after an update):

```xml
<group name="StuntResources">
    <acl name="StuntResources"></acl>
    <object name="resource.stunt_system"></object>
    <object name="resource.stunt_tools"></object>
</group>

<acl name="StuntResources">
    <right name="function.fetchRemote" access="true"></right>
    <right name="function.restartResource" access="true"></right>
</acl>
```

Without `function.fetchRemote` the resources keep working normally; the updater only prints a single clean line to the server console and stays disabled.

## Auto-Update

- 5 seconds after start and every 6 hours each resource reads `github_release/version.json` from the official repository.
- If a newer version exists: a message in the **server console**, a chat message to online **Admins** (version, changelog summary, how to update) and the version badge in the menus turns into `v1.0.0 • New version available` (orange, Admins only).
- **`/atualizarstunt`** (stunt_system) and **`/atualizartools`** (stunt_tools) — Admin only:
  1. downloads every file listed in the release manifest (nothing is written if any download fails);
  2. backs up the current files to `_backup_update/<timestamp>_v<old>/` inside the resource;
  3. replaces the files and restarts the resource (or tells you to `/restart`);
  4. if writing fails, the backup is restored automatically.
- **Never touched:** `*.db`, `config_warp.json`, `replays/`, `replays_publicos/`, `saves/`. Only `.lua` / `.luac` and `.xml` files listed in the manifest are updated (the official channel serves compiled `.luac` files from `updates/<resource>/` in the repository, including a `meta.xml` that references them); binary assets (`.png`, `.mp3`, `.ttf`) are not.
- Manual download: the **Releases** page of the repository (zip per resource).
- Configure the repository once, at the top of each `updater_s.lua` (`manifesto` and `releases`), replacing `Maxral/mta-stunt-suite`.

## Documentation

- [Complete Manual (EN)](docs/MANUAL_COMPLETO_EN.md)
- [Manual Completo (PT)](docs/MANUAL_COMPLETO_PT.md)

## Repository layout

```
stunt_system/
stunt_tools/
updates/
    stunt_system/   (.luac + meta.xml + lang/*.xml)
    stunt_tools/    (.luac + meta.xml + lang/*.xml)
github_release/
    version.json
    README.md
    docs/
```

---

## Português

Dois resources complementares para MTA:SA, voltados a servidores de stunt e criadores de stunts:

| Resource | O que é |
|---|---|
| **`stunt_system`** | Motor das arenas de stunt: markers, conclusão/recordes/ranking, mapa F2 customizado, Gerenciador da Arena (`Alt+F2` / `/stunts`), dificuldades, observações nos stunts, CV Zones. |
| **`stunt_tools`** | Hub de treino e criação: saves/warps (`/sw` `/lw` `/dw`), Hub F7, gravador de Replay / TAS, Galeria de Replays, Modo Ghost com rastro 3D e loop A-B, editor de corte, freecam, HUD velocímetro. |

Funcionam sozinhos, mas compartilham idioma, tema e fonte quando os dois rodam (seletor `PT` / `EN`, temas *Híbrido*, *Moderno*, *Minimalista*, *Clássico*). Versão atual: **v1.0.0**.

### Instalação

1. Copie as pastas `stunt_system` e `stunt_tools` para `server/mods/deathmatch/resources/`.
2. Edite o `server/mods/deathmatch/acl.xml` (veja abaixo) e reinicie o servidor (ou `aclreload`).
3. No console: `refresh`, depois `start stunt_system` e `start stunt_tools`.
4. Adicione os dois ao `mtaserver.conf` para iniciarem sozinhos.

> **Desative outros scripts antigos de Freecam / CamHack que usem a tecla `H`.** O `stunt_tools` já traz freecam + teleporte na `H` (e `R` reparar, `N` nitro, `J` motor). Duas resources na mesma tecla entram em conflito. As teclas mudam em **F7 → Configurações**.

### Configuração obrigatória no `acl.xml`

Os recursos de Admin (comandos de update, `/configwarp`, dificuldades, troca de modo) exigem conta no grupo ACL **Admin** (`<group name="Admin">` com `<object name="user.SuaConta">`). Para o auto-update, os **resources** precisam da permissão `function.fetchRemote` (e `function.restartResource` para se reiniciarem após atualizar) — use os blocos `StuntResources` mostrados acima na seção em inglês.

Sem `function.fetchRemote` tudo continua funcionando; o updater apenas escreve uma linha limpa no console e fica desativado.

### Auto-Update

- 5 s após iniciar e a cada 6 h, cada resource lê o `github_release/version.json` do repositório oficial.
- Com versão nova: aviso no **console**, no **chat dos Admins** (versão, resumo do changelog, como atualizar) e o selo nos menus vira `v1.0.0 • Nova versão disponível` (laranja, só para Admins).
- **`/atualizarstunt`** (stunt_system) e **`/atualizartools`** (stunt_tools) — só Admin: baixa os arquivos do manifesto (nada é gravado se algum download falhar), faz backup em `_backup_update/`, substitui e reinicia o resource; se a gravação falhar, o backup é restaurado.
- **Nunca alterados:** `*.db`, `config_warp.json`, `replays/`, `replays_publicos/`, `saves/`. Só `.lua` / `.luac` e `.xml` do manifesto são atualizados (o canal oficial serve `.luac` compilados em `updates/<resource>/` do repositório, com um `meta.xml` que os referencia) (assets `.png`/`.mp3`/`.ttf` não).
- Download manual: página **Releases** do repositório.
- Configure o repositório uma vez no topo de cada `updater_s.lua` (`manifesto` e `releases`), trocando `Maxral/mta-stunt-suite`.

### Documentação

- [Manual Completo (PT)](docs/MANUAL_COMPLETO_PT.md)
- [Complete Manual (EN)](docs/MANUAL_COMPLETO_EN.md)
