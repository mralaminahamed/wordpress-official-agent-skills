# WordPress Official Agent Skills — Claude Code Plugin

A Claude Code plugin that packages the [official WordPress agent-skills](https://github.com/WordPress/agent-skills) for one-command installation. All 17 skills install automatically — no manual file copying required.

> **Mirror of** [WordPress/agent-skills](https://github.com/WordPress/agent-skills) · GPL-2.0-or-later  
> Original upstream documentation: [README.upstream.md](README.upstream.md)

---

## Installation

```bash
/plugin install wordpress-official-agent-skills/wordpress-official-agent-skills
```

Reload after install:

```bash
/reload-plugins
```

### Pair with wp-dev-skills

These two plugins are designed to coexist without trigger conflicts:

```bash
/plugin install wp-dev-skills/wp-dev-skills
/plugin install wordpress-official-agent-skills/wordpress-official-agent-skills
```

| Plugin | Owns |
|---|---|
| `wp-dev-skills` | Plugin audit, release/version sync, WP.org SVN deploy, PHPStan stubs scaffold, GitHub contribution flow, QA fixes |
| `wordpress-official-agent-skills` | Block development, REST API, WP-CLI ops, Playground, Abilities API, performance, PHPStan config, block themes, Interactivity API |

Boundaries are documented in each plugin's skill trigger descriptions — no ambiguous overlaps.

---

## Included Skills (17)

| Skill | What it covers |
|---|---|
| `wordpress-router` | Classifies WP repos and routes to the right skill automatically |
| `wp-project-triage` | Detects project type, tooling, and WP/PHP versions |
| `wp-plugin-development` | Plugin architecture, hooks, Settings API, security (nonces/caps/escaping/SQL) |
| `wp-plugin-directory-guidelines` | Authoritative review of 18 WP.org Plugin Directory guidelines (GPL, naming, trialware) |
| `wp-block-development` | Gutenberg blocks: `block.json`, attributes, rendering, deprecations |
| `wp-block-themes` | Block themes: `theme.json`, templates, patterns, style variations |
| `wp-interactivity-api` | Frontend interactivity with `data-wp-*` directives and stores |
| `wp-rest-api` | REST routes/endpoints, schema, auth, response shaping |
| `wp-abilities-api` | Capability-based permissions and REST API authentication |
| `wp-abilities-audit` | Audit a plugin's REST surface; propose Abilities API registrations |
| `wp-abilities-verify` | Verify Abilities API registrations against declared annotations |
| `wp-wpcli-and-ops` | WP-CLI commands, automation, multisite, search-replace |
| `wp-performance` | Profiling, caching, DB optimization, Server-Timing |
| `wp-phpstan` | PHPStan config (`phpstan.neon`), baselines, WP-specific type stubs |
| `wp-playground` | WordPress Playground — instant local environments |
| `blueprint` | Playground Blueprints for declarative environment setup |
| `wpds` | WordPress Design System |

---

## How skills activate

Claude Code auto-discovers every `SKILL.md` under `skills/`. Skills activate based on task context matching their `description` field — no manual invocation needed for most workflows. For explicit invocation in another skill or agent, reference by name (e.g. `wp-plugin-development`).

---

## Upstream sync

Skills stay current via a scheduled GitHub Actions workflow that runs every Monday:

- Diffs `skills/` and `shared/` against [WordPress/agent-skills](https://github.com/WordPress/agent-skills) trunk
- Opens a PR if anything changed, with a checklist to verify no new conflicts with `wp-dev-skills`
- `README.upstream.md` is also refreshed from upstream on each sync

To trigger manually:

1. Go to **Actions → Sync Upstream Skills**
2. Click **Run workflow**
3. Optional: enable **Dry run** to preview changes without opening a PR

---

## Plugin structure

```
wordpress-official-agent-skills/
├── .claude-plugin/
│   └── plugin.json          # Claude Code plugin manifest
├── skills/                  # 17 skill directories (auto-discovered)
│   ├── wp-plugin-development/
│   │   ├── SKILL.md
│   │   ├── references/
│   │   └── scripts/
│   └── ...
├── shared/                  # Shared references (WP versions, Gutenberg mapping)
├── .github/workflows/
│   ├── sync-upstream-skills.yml   # Weekly upstream skill sync
│   └── upstream-sync.yml          # Weekly WP core/Gutenberg index refresh
└── README.upstream.md       # Original WordPress/agent-skills README (auto-synced)
```

---

## Contributing

Bug fixes and improvements to the Claude Code plugin layer (manifest, sync workflow, this README) go here.

For skill content improvements — corrections to WordPress patterns, new skill topics, updated references — contribute upstream at [WordPress/agent-skills](https://github.com/WordPress/agent-skills/blob/trunk/CONTRIBUTING.md). Changes flow back here automatically on the next Monday sync.
