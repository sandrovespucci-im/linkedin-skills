# Strato vault: dove vivono voce e materiale

Questo fork è **pubblico**. I dati personali (voce, carriera, numeri, clienti) non
stanno qui: stanno nel vault di Sandro, che è privato. Le skill girano in una
sessione aperta sul vault e leggono questi file con percorsi relativi alla sua
radice.

## I file

| Cosa | File nel vault | Al posto di |
|---|---|---|
| Voce di Sandro (profilo personale, prima persona) | `wiki/synthesis/linkedin-voce-sandro.md` | `references/voice-profile.md` |
| Voce di The I'm (pagina, voce di marca) | `wiki/synthesis/linkedin-voce-theim.md` | `references/voice-profile.md` |
| Story Bank (un'unica banca, la usano entrambe le voci) | `wiki/synthesis/linkedin-story-bank.md` | `references/story-bank.md` |

**Quale voce?** Se Sandro non lo dice, chiedilo una volta prima di scrivere:
profilo personale o pagina The I'm. Non mescolare le due in una bozza.

Se un file non esiste o ha `filled: no`, la skill procede con le regole di voce
generiche e lo dice una volta.

## Il vault prima delle domande

Molto del materiale che l'Interviewer chiederebbe è già scritto. Prima di fare
una domanda, cerca (`./cli.sh search <query>` o grep su `wiki/` e `daily/`):

- [[stato-attuale]] e [[storico-evolutivo]]: cosa è successo, quando;
- le schede in `wiki/entities/`: persone e aziende, con cosa si può dire;
- [[project-personal-branding-linkedin]], [[linkedin-monitor]]: post già
  pubblicati e loro numeri;
- `assets/social/setup-pubblicazione.md`: identità e promessa pubblica di Sandro
  ("Non spiego niente che non abbia fatto girare").

Poi chiedi solo i buchi. Nella Story Bank si scrive **il puntatore alla canonica
più la frase viva**, non una copia del fatto (regola anti-duplicazione del vault).

## Vincoli del vault che le skill rispettano sempre

Le skill girano in una sessione aperta sul vault, quindi il `CLAUDE.md` del vault
e le sue regole (`.claude/rules/`) sono già in contesto. **Valgono tutte, e
prevalgono su questo fork.** In particolare, prima di ogni bozza:

- **Anti-leak.** Nessun contenuto da pagine con tag `personale` entra in una
  bozza, nella Story Bank o in un file di questo fork. Tassativo.
- **Fonti.** Un numero, una data, un nome entrano in un post solo se verificati
  alla fonte nel vault. In dubbio si chiede, o si scrive in forma cauta.
  L'Interviewer non inventa e non deduce.
- **Narrativa e gate di pubblicazione.** Come si racconta il prodotto, cosa si
  può nominare e quando un materiale esterno può uscire lo decidono le
  priorità del `CLAUDE.md` del vault. Una bozza che non le rispetta si scrive
  ma non si pubblica: lo si dice a Sandro.
- **Regole editoriali.** [[pipeline-pubblicazione-social]] §2 (niente hashtag su
  LinkedIn, fatti verificati prima di scrivere, niente CTA nelle immagini).
- **Linguaggio superato.** Prima di riusare materiale vecchio, controlla
  [[glossario-linguaggio-superato]].
- **Clienti e prospect.** Un nome in un post solo se la sua scheda (o la sezione
  "Nomi utilizzabili" della Story Bank) lo consente.

Questo file resta generico di proposito: il fork è pubblico, la strategia sta nel vault.
