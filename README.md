# linkedin-skills — fork `theim`

Fork di [sergebulaev/linkedin-skills](https://github.com/sergebulaev/linkedin-skills) (MIT), adattato per
**Sandro Vespucci** (profilo personale) e **The I'm** (pagina). Ramo di lavoro: `theim`.

## Cosa cambia rispetto all'upstream

- **Niente layer a pagamento.** Via Apify, Publora e Pixfaro (e la libreria `lib/` che li chiamava).
  - Lettura dei post e pubblicazione: dal **browser interno di Claude**, con una conferma esplicita
    per ogni oggetto pubblicato → [`references/strato-browser.md`](references/strato-browser.md)
  - Immagini: composizione HTML → PNG nel look del brand pubblico →
    [`references/strato-immagini.md`](references/strato-immagini.md)
- **I dati personali non stanno qui.** Il fork è pubblico. Le due voci (Sandro, The I'm) e la Story Bank
  vivono nel vault privato; i file in `references/` sono solo puntatori →
  [`references/strato-vault.md`](references/strato-vault.md)
- **9 skill invece di 12.** Tolte employee-advocacy, engager-analytics e thread-monitor.
- **Italianizzazione:** in corso (regole di voce, scrub dell'AI, formule di hook).

## Le skill

| Skill | A cosa serve |
|---|---|
| `linkedin-interviewer` | Riempie la Story Bank: prima legge il vault, poi chiede solo i buchi |
| `linkedin-post-writer` | Scrive un post da zero, con le formule di hook |
| `linkedin-humanizer` | Toglie i tic dell'AI; `--mode audit` prima di pubblicare; `--mode profile` costruisce la voce |
| `linkedin-profile-optimizer` | Riscrive headline, About, Featured, Esperienze |
| `linkedin-comment-drafter` | Commento (o repost con commento) su un post altrui |
| `linkedin-reply-handler` | Risposte a un commento, o a un intero thread |
| `linkedin-hook-extractor` | Estrae la formula di hook da un post che ha funzionato |
| `linkedin-content-planner` | Piano di una settimana |
| `linkedin-repurposer` | Da articolo, carosello o video a post LinkedIn nativo |

## Installazione (Windows)

Le skill si collegano a `~/.claude/skills` con delle **junction** (niente symlink, niente Modalità
sviluppatore). Si usano in una sessione aperta sul vault.

## Aggiornamenti dall'upstream

```bash
git fetch upstream
```

Poi si valuta cosa portare su `theim`: i file toccati qui (skill, `references/strato-*`, puntatori) vanno
riconciliati a mano.
