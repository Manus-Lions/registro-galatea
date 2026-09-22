# Registro dei giudizi

Un'app per annotare coppie di giudizio, ragionamenti completi e problemi del banco di prova, in vista del fine-tuning e del DPO. Le annotazioni vengono salvate in un repository **privato** su GitHub: ogni salvataggio è un commit, quindi resta la storia completa di ogni modifica.

## Come è fatta

Sono due cose separate:

- **L'app** (`index.html`): un'unica pagina, senza dati dentro. Può stare su GitHub Pages oppure essere aperta direttamente dal tuo Mac.
- **Il repository dei dati** (privato): contiene le annotazioni. L'app ci scrive attraverso un token personale che vive solo nel tuo browser.

Nel repository dei dati troverai:

```
annotazioni/2026-09.json      le annotazioni, un file per mese
annotazioni/2026-10.json
esportazioni/dpo.jsonl        pronti per TRL, aggiornati dal pulsante
esportazioni/sft.jsonl        «Aggiorna i file nel repository»
esportazioni/banco-di-prova.jsonl
```

## 1. Crea il repository dei dati

1. Su GitHub: **New repository**.
2. Nome: per esempio `registro-dati`.
3. Visibilità: **Private**.
4. Spunta **Add a README file** (serve a creare il ramo `main`).
5. **Create repository**.

## 2. Crea il token di accesso

1. Foto profilo in alto a destra → **Settings** → **Developer settings** (in fondo a sinistra) → **Personal access tokens** → **Fine-grained tokens** → **Generate new token**.
2. Nome: `registro-giudizi`. Scadenza: scegli tu (per esempio un anno), e segnati di rinnovarlo.
3. **Repository access** → **Only select repositories** → scegli solo `registro-dati`.
4. **Permissions** → **Repository permissions** → **Contents** → **Read and write**. Nient'altro.
5. **Generate token** e copialo subito: GitHub lo mostra una volta sola.

Con questi permessi il token può leggere e scrivere solo in quel repository, e non può fare altro sul tuo account.

## 3. Metti online l'app (oppure no)

**Opzione A, la più semplice:** tieni `index.html` sul Mac e aprilo con doppio clic. Funziona lo stesso: salva su GitHub come la versione online.

**Opzione B, su GitHub Pages**, per aprirla da qualunque dispositivo:

1. Crea un secondo repository, per esempio `registro-app`. Con l'account gratuito GitHub Pages richiede che sia **pubblico**: non è un problema, perché contiene solo il codice dell'app e nessun dato. Chi trovasse l'indirizzo vedrebbe un'app vuota, inutilizzabile senza il tuo token.
2. **Add file** → **Upload files** → carica `index.html` → **Commit changes**.
3. **Settings** → **Pages** → **Source: Deploy from a branch** → ramo `main`, cartella `/ (root)` → **Save**.
4. Dopo un paio di minuti l'app è su `https://TUONOME.github.io/registro-app/`. La pagina chiede ai motori di ricerca di non indicizzarla.

## 4. Primo avvio

1. Apri l'app. Si apre il riquadro **Collegamento al repository dei dati**.
2. Inserisci il tuo nome utente GitHub, `registro-dati`, ramo `main`, e il token.
3. **Collega e carica**. In alto a destra deve comparire «Salvato su GitHub».
4. Se avevi annotazioni nel registro locale precedente, esporta lì un backup e importalo qui con **Importa file…**.

Su ogni altro dispositivo (un secondo computer, il telefono) ripeti solo il punto 2 e 3.

## Uso quotidiano

- Ogni annotazione salvata, modificata o eliminata viene scritta subito su GitHub. Se sei offline, l'app tiene la modifica nel browser e mostra «Riprova»: al primo collegamento la invia.
- Se modifichi dallo stesso registro su due dispositivi, le versioni vengono unite annotazione per annotazione, tenendo la più recente.
- Un'annotazione eliminata resta recuperabile nella storia del repository (**Commits**).
- Quando vuoi addestrare, premi **Aggiorna i file nel repository**: i tre file JSONL in `esportazioni/` sono quelli da usare.

## Sicurezza e conservazione

- Il token è salvato nel browser del dispositivo. Non collegare l'app su computer condivisi; se perdi un dispositivo, revoca il token dalle impostazioni GitHub e creane uno nuovo.
- **Scollega questo dispositivo** cancella il collegamento da quel browser.
- Per una seconda copia indipendente, clona `registro-dati` sul Mac con GitHub Desktop e aggiornala ogni tanto con **Fetch**: avrai l'intero registro, storia compresa, anche fuori da GitHub.
