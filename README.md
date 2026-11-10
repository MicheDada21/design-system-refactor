# design-system-refactor

Sposta gli stili scritti a mano nei token e l'interfaccia ripetuta in componenti condivisi, con la prova che ogni pagina resta identica al pixel.

Fa parte della [Prompt Library di CH Labs](https://www.cryptohelvetia.com/ch-labs/prompt-library), dove la pagina di riferimento è [Design system refactor](https://www.cryptohelvetia.com/ch-labs/prompt-library/skills/design-system-refactor). Il repo contiene una copia della skill, rigenerata a ogni aggiornamento della libreria.

## Installare

In Claude Code aggiungi una volta il marketplace e installa il plugin.

```
/plugin marketplace add MicheDada21/ch-labs-skills
/plugin install design-system-refactor@ch-labs-skills
```

Da shell i comandi sono `claude plugin marketplace add MicheDada21/ch-labs-skills` e `claude plugin install design-system-refactor@ch-labs-skills`. Nell'app desktop premi + accanto al campo del prompt, apri Plugins, aggiungi il marketplace `MicheDada21/ch-labs-skills` con Add marketplace e poi il plugin con Add plugin.

Per avere tutte le skill della libreria installa `tutte-le-skill@ch-labs-skills`. Con altri agenti copia la cartella `skills/design-system-refactor` tra le skill dell'agente, per esempio in `~/.codex/skills/design-system-refactor`.

## Licenza

MIT, testo completo in [LICENSE](LICENSE).
