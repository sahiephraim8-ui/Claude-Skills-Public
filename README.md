# Claude-Skills-Public

Bibliothèque de **288 skills Claude** sélectionnés, audités et organisés — couvrant tous les domaines pro d'un founder : stratégie & C-level, sales & revenue, finance, crypto & trading, marketing & growth, produit, opérations, recherche, data, design UI/UX, animation & 3D, automatisation n8n, méthodologie d'ingénierie, et productivité.

> Backup versionné du stock de skills actifs (`~/.claude/skills/`). Chaque skill est un dossier `skills/<nom>/` contenant un `SKILL.md` (frontmatter `name` + `description`) et ses fichiers de support (assets/references/scripts).

## Installation

Copier un skill dans le dossier des skills de Claude Code :

```bash
cp -r skills/<nom-du-skill> ~/.claude/skills/
```

Le skill devient actif automatiquement (Claude le déclenche selon sa `description`).

## Organisation par domaine

| Domaine | Exemples de skills |
|---|---|
| **Design UI/UX** | `taste-skill`, `claude-design-skill`, `bencium-impact-designer`, `design-audit`, `redesign-skill`, `modern-web-design`, `typography`, `minimalist-skill`, `brutalist-skill`, `soft-skill`, `stitch-skill`, `brandkit` |
| **Animation & 3D** | `gsap-scrolltrigger`, `motion-framer`, `animejs`, `threejs-webgl`, `react-three-fiber`, `babylonjs-engine`, `spline-interactive`, `lottie-animations`, `rive-interactive` |
| **Stratégie & C-level** | `ceo-advisor`, `cfo-advisor`, `coo-advisor`, `cmo-advisor`, `cto-advisor`, `chief-of-staff`, `executive-mentor`, `scenario-war-room`, `ma-playbook`, `org-health-diagnostic` |
| **Commercial & Revenue** | `pricing-strategist`, `deal-desk`, `commercial-forecaster`, `rfp-responder`, `revenue-operations`, `sales-engineer`, `customer-success-manager`, `cold-email` |
| **Finance** | `financial-analyst`, `saas-metrics-coach`, `business-investment-advisor` |
| **Marketing** | `copywriting`, `marketing-psychology`, `content-humanizer`, `paid-ads`, `launch-strategy`, `x-twitter-growth`, `competitive-ads-extractor` |
| **Produit & Recherche** | `product-strategist`, `product-discovery`, `competitive-teardown`, `jtbd`, `ux-researcher-designer`, `market-research`, `dossier`, `litreview`, `research-summarizer` |
| **Méthodologie (Superpowers)** | `brainstorming`, `systematic-debugging`, `root-cause-tracing`, `writing-plans`, `test-driven-development`, `dispatching-parallel-agents`, `when-stuck` |
| **Crypto & on-chain** | `coingecko-api`, `dexscreener-api`, `whale-tracking`, `wallet-profiling`, `mev-analysis`, `dex-pool-analysis`, `impermanent-loss`, `yield-analysis`, `solana-rpc`, `pumpfun-mechanics`, `sybil-detection`, `copy-trading` |
| **Trading & quant** | `backtest-expert`, `backtrader`, `vectorbt`, `ta-lib`, `pandas-ta`, `mean-reversion`, `regime-detection`, `kelly-criterion`, `position-sizing`, `risk-management`, `volatility-modeling`, `options-pricing`, `walk-forward-validation`, `vcp-screener`, `canslim-screener`, `technical-analyst`, `portfolio-manager` |
| **Automatisation n8n** | `n8n-workflow-patterns`, `n8n-node-configuration`, `n8n-expression-syntax`, `n8n-code-javascript`, `n8n-code-python`, `n8n-code-tool`, `n8n-mcp-tools-expert`, `n8n-validation-expert` |
| **Data & Compliance** | `statistical-analyst`, `senior-data-scientist`, `data-quality-auditor`, `rag-architect`, `rag-eval`, `gdpr-audit-prep`, `soc2-audit-prep` |
| **Productivité & Docs** | `capture`, `reflect`, `decision-toolkit`, `pdf-generation`, `tufte-report`, `meeting-analyzer`, `contract-and-proposal-writer` |

## Crédits & sources

Ces skills proviennent de la communauté open-source Claude. Chaque dossier conserve sa licence d'origine quand elle est fournie. Sources principales :

- [anthropics/skills](https://github.com/anthropics/skills) — skills officiels
- [obra/superpowers-skills](https://github.com/obra/superpowers-skills) & [obra/superpowers-lab](https://github.com/obra/superpowers-lab) — Jesse Vincent
- [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills)
- [Leonxlnx/taste-skill](https://github.com/Leonxlnx/taste-skill)
- [bencium/bencium-marketplace](https://github.com/bencium/bencium-marketplace)
- [freshtechbro/claudedesignskills](https://github.com/freshtechbro/claudedesignskills)
- [jiji262/claude-design-skill](https://github.com/jiji262/claude-design-skill)
- [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills)
- [glebis/claude-skills](https://github.com/glebis/claude-skills)
- [czlonkowski/n8n-skills](https://github.com/czlonkowski/n8n-skills) — Romuald Czlonkowski (auteur de `n8n-mcp`)
- [swarmclawai/andrej-karpathy-skills](https://github.com/swarmclawai/andrej-karpathy-skills)

Tous les crédits reviennent aux auteurs originaux. Ce dépôt est une collection curatée à usage personnel et de partage.
