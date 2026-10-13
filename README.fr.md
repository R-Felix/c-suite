# c-suite (en français)

**Mener n'importe quel projet comme une entreprise bien dirigée.** Tu es le dirigeant : le *quoi* t'appartient.
Claude est l'orchestrateur, ton COO : il s'occupe du *comment* et dirige une équipe d'agents par rôle, chacun avec le
bon modèle et le bon effort pour sa tâche.

Le plugin est écrit en anglais pour être partagé, mais **il travaille dans ta langue** : ton profil
(`~/.claude/c-suite/principal.md`) fixe la langue de chaque message et de chaque document du projet. Seuls les noms
de fichiers restent en anglais, pour que les skills les retrouvent. Tu peux parler à Claude en français : « démarre un
projet », « planifie le jalon 2 », « on fait une pause », « reprends », « aide-moi à trancher ».

## Les skills

| Skill | Quand | Ce qu'il fait |
|---|---|---|
| `/c-suite:start-project` | Le premier jour | Une courte entrevue, puis la charte (résultat visé, mesures de succès, budget, hors-portée, pré-mortem), la définition de « fini », la feuille de route, le journal des décisions, le registre des coûts et le cadre des agents |
| `/c-suite:plan-milestone` | Avant chaque jalon | Les cartes de tâche (le cahier des charges de chaque agent), avec l'estimation du coût et l'heure de fin |
| `/c-suite:run-milestone` | Pendant | La boucle du COO : deux agents au plus, acceptation sur preuve, registre des coûts, décisions, règles du jour et de la nuit |
| `/c-suite:handoff` | Pause ou reprise | L'état du projet, pour qu'une session neuve reprenne sans relancer un gros contexte |
| `/c-suite:retrospective` | Après chaque jalon | Bilan sans blâme; règles promues au projet, à la maison ou à c-suite; choix des modèles recalibré |
| `/c-suite:decision-brief` | Une décision difficile | Une page : options comparées, recommandation, le test peu coûteux qui tranche |

Les six rôles d'agents et leurs modèles : `scout` (Haiku, effort bas), `builder` (Sonnet, moyen), `specialist` (Opus,
élevé), `architect` (Opus, très élevé), `reviewer` (Sonnet, élevé), `expert` (Fable, élevé, en réserve).

## Le jour et la nuit

Claude lit l'heure. Pendant tes heures de travail, il pose ses questions, groupées et numérotées. En dehors, il ne
t'attend jamais et ne t'envoie aucune notification : il tranche ce qui se défait, met de côté ce qui ne se défait pas,
et t'accueille au matin avec la liste numérotée des décisions à confirmer ou à renverser.

## Installer

```bash
claude plugin marketplace add OWNER/c-suite
claude plugin install c-suite@c-suite
```

Puis, dans un dossier vide ou un projet existant : `/c-suite:start-project`. La première fois, quelques questions sur
toi (nom, langue, heures de travail, notifications, budget) écrivent ton profil. Claude Code demande une fois par
projet d'autoriser l'import de ce profil dans le `CLAUDE.md` du projet : accepte.

Le détail est dans le [README anglais](README.md).
