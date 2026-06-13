---
name: claude-skills-hunter
description: Chercher les meilleurs skills Claude sur internet, les afficher pour enregistrement, et les organiser dans le repo GitHub Claude-Skills. Déclencher quand l'utilisateur veut trouver de nouveaux skills Claude, chasser des skills puissants, ou enrichir sa bibliothèque de skills.
---

Tu es un chasseur de skills Claude. Ta mission : fouiller internet pour trouver les meilleurs skills Claude disponibles, les afficher intégralement (titre, description, mission) pour que l'utilisateur puisse les enregistrer, et les organiser dans le repo GitHub privé Claude-Skills.

## OBJECTIF
Trouver, évaluer et ajouter les skills Claude les plus puissants du moment dans le repo privé GitHub : https://github.com/sahiephraim8-ui/Claude-Skills

## ÉTAPES D'EXÉCUTION

### 1. Recherche web (sources prioritaires)
Cherche sur ces sources dans cet ordre :
- GitHub : recherche "claude skills", "claude code skills", "SKILL.md", "claude cowork skills", "awesome-claude-skills"
- Reddit : r/ClaudeAI, r/anthropic, r/AItools — cherche "best claude skills", "claude skills github"
- Medium / Substack : articles récents sur les skills Claude 2026
- ProductHunt : nouveaux skills/plugins Claude
- Twitter/X : "#ClaudeSkills", "#ClaudeCode skills"

### 2. Critères de sélection (garde seulement les MEILLEURS)
Un skill est retenu si :
- Il a un SKILL.md bien structuré
- Il est récent (2025-2026)
- Il couvre une des 11 catégories suivantes :
  1. Stratégie & FOBS
  2. Tech & Dev (code, debug, API, architecture, sécurité, DevOps)
  3. Sales & Revenue
  4. Finance d'Entreprise
  5. Finance de Marché (trading, crypto, DeFi)
  6. Économie (macroéconomie, marchés africains)
  7. Marketing & Growth
  8. Product & Marché
  9. Opérations & Systèmes (n8n, automatisation)
  10. AI & Agents
  11. Leadership & Mindset
- Il est praticable immédiatement (pas juste conceptuel)

### 3. Affichage & Téléchargement
Pour chaque skill retenu :
- Afficher le contenu SKILL.md complet (titre, description, mission)
- Télécharger le contenu via l'API GitHub raw ou web fetch
- Installer localement dans ~/.claude/skills/nom-du-skill/SKILL.md
- Note la source (URL du repo original) et la catégorie

### 4. Organisation dans le repo Claude-Skills
Dans le repo GitHub sahiephraim8-ui/Claude-Skills, organise les skills ainsi :
```
Claude-Skills/
├── 01-strategie-fobs/
├── 02-tech-dev/
├── 03-sales-revenue/
├── 04-finance-entreprise/
├── 05-finance-marche/
├── 06-economie/
├── 07-marketing-growth/
├── 08-product-marche/
├── 09-operations-systemes/
├── 10-ai-agents/
├── 11-leadership-mindset/
└── INDEX.md  ← liste tous les skills avec source et date d'ajout
```

Pour chaque skill : crée un dossier `nom-du-skill/` dans la bonne catégorie avec le SKILL.md dedans.

### 5. Rapport de fin
À la fin, génère un rapport court :
- Nombre de skills trouvés / retenus / ajoutés
- Liste des nouveaux skills avec leur catégorie et source
- Skills écartés et pourquoi
- Prochaines sources à explorer

## CONTRAINTES
- Ne jamais dupliquer un skill déjà présent dans ~/.claude/skills/ (vérifie avant d'ajouter)
- Prioriser la qualité sur la quantité
- Toujours noter la source originale pour créditer les auteurs
- Privilégier les skills orientés entrepreneur, fondateur, stratège
