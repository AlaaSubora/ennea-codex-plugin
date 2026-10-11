# Ennea for Codex

Install **Ennea**, choose **Connect**, sign in to Ennea and select the workspace,
actions and record types to allow. Codex manages the OAuth credentials. You do not
need Node, a local MCP server, a token pasted into chat, or an npm package.

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

The marketplace is `.agents/plugins/marketplace.json`. The plugin supports both
the portable manifest and Codex's compatibility manifest. Open its connection
settings and authenticate. Run its setup skill to verify the actual identity,
workspace and capabilities. Installed tools alone do not prove a working account
connection. Public directory listing is a separate submission process.

Access tokens last fifteen minutes and rotate through refresh tokens. Connections
last at most thirty days and remain bound to the issuing browser session and
current permissions. Signing out, session expiry, revocation or losing workspace
access disconnects the agent. Reconnect through Codex to change the workspace or
the consented access. Credentials and session identifiers never belong in prompts.

## Maintainer packaging and verification

The checked-in package uses the hosted production endpoint. For another deployment:

```sh
pnpm --filter @ennea/agent-adapter plugin:build \
  --mcp-url https://your-deployment.example/mcp \
  --output /absolute/new/marketplace-directory
```

`--locale de` selects German install copy. The output directory must be new.
`--allow-loopback` permits local developer tests. URLs containing credentials,
queries or fragments are rejected. Packaging does not deploy a backend.

The backend serves protected-resource and authorization-server discovery, PKCE
consent, code exchange, refresh and revocation. Apply and verify
`pnpm --filter @ennea/backend agent-operations:indexes` in the explicit target
database using its dry-run/apply/verify modes before accepting connections.
See the [public plugin project](https://github.com/AlaaSubora/ennea-codex-plugin)
for installation and connection guidance.

## Deutsch

Installiere **Ennea**, wähle **Verbinden**, melde dich bei Ennea an und wähle den
Arbeitsbereich, die erlaubten Aktionen und Datensatztypen. Codex verwaltet die
OAuth-Zugangsdaten. Du brauchst keinen lokalen Server, kein npm-Paket und keine
Zugangsdaten im Chat.
Installiere das Plugin über den öffentlichen Marketplace
`AlaaSubora/ennea-codex-plugin`. Du brauchst keinen Zugriff auf das
Ennea-Anwendungsrepository.

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
