# Strato immagini

Sostituisce Pixfaro. Le immagini le genera Claude, con la stessa catena
già in produzione per i canali The I'm: **composizione HTML → render PNG/JPEG**.
Processo e regole canoniche nel vault: [[pipeline-pubblicazione-social]];
look in [[theim-design-system]] §0 bis.

## Regole (dal vault, non negoziabili)

- **La foto è informativa, il commento è personale.** L'immagine porta il fatto
  verificabile (un numero, uno schema, una citazione); opinione e voce stanno nel
  testo del post. Niente immagini-slogan.
- **Il look si legge dal canale, non da una skill.** Design system pubblico:
  arancio `#E8650A` + viola `#7D6DFF`, font Outfit + DM Sans. La skill
  `the-im-instagram` porta una palette morta: non usarla come fonte.
- **Il file approvato è il file pubblicato.** Niente ri-render dopo il sì.
- **Niente CTA nell'immagine.**

## Formati LinkedIn

| Uso | Dimensioni |
|---|---|
| Post, immagine singola orizzontale | 1200×627 |
| Post, quadrata | 1080×1080 |
| Post, verticale (resa migliore nel feed mobile) | 1080×1350 |
| Banner profilo | 1584×396 |

## Tipi

- **Quote-card**: una riga del post (di solito l'hook o il numero) composta in
  tipografia. Testo vero, non disegnato da un modello: niente refusi.
- **Schema / dato**: un numero con il suo riferimento, un prima/dopo, un
  diagramma semplice.
- **Carosello (PDF)**: più slide 1080×1350 esportate in un PDF.

## Dove stanno i file

Sorgente HTML e render in `assets/social/linkedin/` del vault. I binari di
passaggio in `_transfer/` (gitignored). Esempi esistenti:
`card_iceberg_strumenti_1080.html`.

Per allegare l'immagine al post: `strato-browser.md` §Immagini da allegare.
