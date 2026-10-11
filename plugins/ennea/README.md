# Ennea for Codex

Install **Ennea**, connect through Codex's connection controls, sign in to Ennea
and select the workspace, actions and record types to allow. Codex manages the
OAuth credentials. You do not need Node, a local MCP server, a token pasted into
chat, or an npm package.

The plugin connects to `https://api.ennea-ai.com/mcp` and includes setup and work
skills. Source exploration stays in your agent environment. Send native structured
operations individually or in batches; review the resulting drafts in Ennea.
The listing and composer use Ennea's bundled landing-page logo.
Agents cannot approve their own proposals. You can revoke a connection under
**Agents → Agent access**.

## Install from the Ennea marketplace

Add the public Ennea plugin marketplace and install Ennea. You do not need access
to Ennea's application repository.

```sh
codex plugin marketplace add AlaaSubora/ennea-codex-plugin --ref main
codex plugin add ennea@ennea
```

The marketplace is `.agents/plugins/marketplace.json`. The public Codex package
uses `.codex-plugin/plugin.json`, `.mcp.json`, bundled skills, and logo assets.
Authenticate through the host's Ennea connection controls. After installation or
a package update, restart the desktop host and start a **new chat** with Ennea
enabled. Run its Setup skill there to verify the actual identity, workspace, and
capabilities.
Public directory listing is a separate submission process.

To fetch marketplace updates, refresh its source in the host or use
`codex plugin marketplace upgrade ennea`. Check the installed version before
restarting and testing in a new chat. These checks follow the
[official packaging guidance](https://developers.openai.com/plugins/build/plugins)
and [complete-plugin testing guidance](https://developers.openai.com/plugins/deploy/connect-chatgpt).

## Check Setup and connection problems

Setup succeeds when `ennea_context` and `ennea_capabilities` return the actual
connected workspace and permitted operations. A visible plugin or Setup skill
does not by itself establish that the chat can call those tools.

If Setup reports that Ennea tools are unavailable, check that Ennea is enabled,
refresh the marketplace source, restart the desktop host, and retry in a **new
chat**. Missing tools alone do not establish an OAuth error. If the tools remain
unavailable, report the installed version and exact error through the support
links below. These checks do not guarantee a fix for every host issue.

If an available tool returns **Auth required** or HTTP 401, reconnect Ennea through
the host's connection controls and complete browser sign-in and consent. If an
action or record type is forbidden, check the consented access and current Ennea
permissions. Keep passwords and OAuth tokens out of chat.

Find help in the [Ennea FAQ](https://www.ennea-ai.com/faq/) or through the
[Ennea contact details](https://www.ennea-ai.com/impressum/).

Access tokens last fifteen minutes and rotate through refresh tokens. Connections
last at most thirty days and remain bound to the issuing browser session and
current permissions. Signing out, session expiry, revocation or losing workspace
access disconnects the agent. Reconnect through Codex to change the workspace or
the consented access. Credentials and session identifiers never belong in prompts.

## Maintainer packaging and verification

The builder produces the Codex compatibility layout by default. Its hosted MCP
configuration is in `.mcp.json`; the manifest is `.codex-plugin/plugin.json`.
For another deployment:

```sh
pnpm --filter @ennea/agent-adapter plugin:build \
  --mcp-url https://your-deployment.example/mcp \
  --output /absolute/new/marketplace-directory
```

`--locale de` selects German install copy. The output directory must be new.
`--allow-loopback` permits local developer tests. URLs containing credentials,
queries or fragments are rejected. Packaging does not deploy a backend.

Maintainers can explicitly generate a portable Agent Plugins package for a host
that supports that format:

```sh
pnpm --filter @ennea/agent-adapter plugin:build \
  --format portable \
  --mcp-url https://your-deployment.example/mcp \
  --output /absolute/new/portable-marketplace-directory
```

That format uses root `plugin.json` and `mcp.json`. Keep the public Codex marketplace
on the default compatibility output and verify actual skill and tool calls after
every package update.

The backend serves protected-resource and authorization-server discovery, PKCE
consent, code exchange, refresh and revocation. Apply and verify
`pnpm --filter @ennea/backend agent-operations:indexes` in the explicit target
database using its dry-run/apply/verify modes before accepting connections.
See the [public plugin project](https://github.com/AlaaSubora/ennea-codex-plugin)
for installation and connection guidance.

## Deutsch

Installiere **Ennea**, verbinde dein Ennea-Konto über die Verbindungsfunktionen von
Codex, melde dich im Browser an und wähle den Arbeitsbereich, die erlaubten Aktionen
und Datensatztypen. Codex verwaltet die OAuth-Zugangsdaten. Du brauchst keinen
lokalen Server, kein npm-Paket und keine Zugangsdaten im Chat.
Installiere das Plugin über den öffentlichen Marketplace
`AlaaSubora/ennea-codex-plugin`. Du brauchst keinen Zugriff auf das
Ennea-Anwendungsrepository.

Das öffentliche Codex-Paket enthält `.codex-plugin/plugin.json`, `.mcp.json`, die
Skills und die Logo-Dateien. Der Paket-Builder erzeugt dieses Codex-Format
standardmäßig. Mit `--format portable` können Maintainer ein separates Paket mit
`plugin.json` und `mcp.json` für einen Host erzeugen, der das portable Format
unterstützt. Für den öffentlichen Codex-Marketplace verwenden wir die
standardmäßige Codex-Ausgabe.

Aktualisiere nach einer Paketänderung die Marketplace-Quelle im Host oder mit
`codex plugin marketplace upgrade ennea` und prüfe die installierte Version.
Starte die Desktop-App nach der Installation oder Aktualisierung neu und öffne
einen **neuen Chat**, in dem Ennea aktiviert ist. Führe dort den Setup-Skill aus.
Setup ist erfolgreich, wenn `ennea_context` und `ennea_capabilities` den
tatsächlichen Arbeitsbereich und die erlaubten Aktionen zurückgeben. Ein
sichtbares Plugin oder ein vorhandener Skill beweist diesen Zugriff noch nicht.

Wenn Setup keine Ennea-Tools im Chat findet, prüfe die Aktivierung, aktualisiere
die Marketplace-Quelle und teste nach einem Neustart in einem neuen Chat. Diese
Meldung allein belegt keinen OAuth-Fehler. Wenn die Tools weiterhin fehlen, melde
die installierte Version und die genaue Fehlermeldung über die Hilfe-Links.
Diese Schritte garantieren nicht die Behebung jedes Host-Problems.

Wenn ein verfügbares Tool **Auth required** oder HTTP 401 zurückgibt, verbinde
Ennea über die Verbindungsfunktionen des Hosts erneut und durchlaufe die Anmeldung
und Freigabe im Browser. Bei einer verweigerten Aktion oder einem gesperrten
Datensatztyp prüfe die erteilte Freigabe und deine aktuellen Ennea-Berechtigungen.
Teile keine Passwörter oder OAuth-Tokens im Chat. Hilfe findest du in den
[häufigen Fragen](https://www.ennea-ai.com/faq/) und über die
[Ennea-Kontaktdaten](https://www.ennea-ai.com/impressum/).

Dein Agent verarbeitet Quelldaten in seiner eigenen Umgebung und übergibt
strukturierte Änderungen einzeln oder als Paket. Prüfe die Entwürfe in Ennea,
bevor du sie anwendest. Ein Agent kann seine Vorschläge nicht selbst freigeben.
Das Plugin und der Chat-Eingabebereich zeigen das Logo der Ennea-Website.
Widerrufe den Zugriff jederzeit unter **Agenten → Agentenzugriff**. Die Verbindung
endet spätestens nach 30 Tagen oder früher, wenn du dich abmeldest, deine Sitzung
abläuft oder deine Berechtigungen entfallen. Verbinde dein Konto erneut, um den
Arbeitsbereich oder die erlaubten Aktionen zu ändern.

## Format references

- [Plugin packaging and marketplaces](https://developers.openai.com/plugins/build/plugins)
- [MCP authentication and OAuth](https://developers.openai.com/plugins/build/auth)
