# Esercitazione 0 — Compilazione, esecuzione e Git

Riprendiamo la compilazione e l'esecuzione di un programma C, già affrontate l'anno scorso, e vediamo come ricevere argomenti attraverso `argc` e `argv`. Useremo **Git** per registrare le versioni del lavoro, **GitHub** per condividerle con il docente e **Classroom 50** per accettare l'esercitazione e verificarne la consegna.

Lavora **in locale**, sulla copia del repository assegnato clonata sul tuo computer. Puoi usare GCC e gli altri strumenti installati sul computer.

## Step 0 — Accettare l'esercitazione e preparare Git

### Primo accesso

1. Crea un account su [GitHub](https://github.com), se non ne hai già uno, e comunica il tuo username al docente per essere inserito nella classe.
2. Accetta l'invito all'organizzazione GitHub del corso.
3. Vai sul sito del docente ([https://www.roma1.infn.it/~rovigatl](https://www.roma1.infn.it/~rovigatl)), e da lì alla pagina del corso ([Didattica -> Laboratorio di Fisica Computazionale](https://www.roma1.infn.it/~rovigatl)).
4. Scarica il file linkato in fondo, utilizzate il terminale per andare nella cartella dove è stato scaricato ed eseguitelo con il comando `bash LFC1_install.sh`.
5. Chiudi e riapri il terminale (o apri un'altra tab) e lancia il comando `github-inizio.sh`. **Questo comando andrà dato ogni volta che cominciate un'esercitazione**.
6. **Nel terminale**, inserisci il tuo username GitHub, non l'email né il nome dell'utente Linux. Se viene chiesto di autenticare anche Git, rispondi `Yes`.
7. **Prendi il codice dal terminale.** Prima di aprire il browser, `gh` mostra una riga simile a questa:
   ```text
   First copy your one-time code: XXXX-XXXX
   ```
   Copia o annota il codice effettivamente mostrato, poi premi Invio se richiesto per aprire il browser. `XXXX-XXXX` è solo un esempio del formato, non un codice da usare.
8. **Nel browser, accedi al tuo account GitHub.** Se non sei già autenticato, inserisci le tue credenziali. **Quando GitHub chiede il codice di autenticazione a due fattori (2FA), devi inserire anche quello:** prendilo dall'app di autenticazione configurata per il tuo account, oppure dal metodo che hai impostato, per esempio SMS. Se usi una passkey o una chiave di sicurezza, segui la relativa richiesta. Se la sessione del browser è già autenticata, questo passaggio potrebbe non comparire.
9. **Nella pagina "Device Activation" / "Authorize your device"**, inserisci il codice `XXXX-XXXX` che hai preso **dal terminale** e premi **Continue**. Controlla che "Signed in as" mostri il tuo username.
10. Conferma l'autorizzazione a **GitHub CLI**, seguendo il pulsante mostrato nella pagina.
11. **Torna al terminale** e attendi `Accesso GitHub pronto per ...`. Verifica il nome prima di iniziare a lavorare.

I due codici non sono intercambiabili:

| Codice richiesto | Dove prenderlo | Dove inserirlo |
| --- | --- | --- |
| Codice di autenticazione a due fattori (2FA), se richiesto | Dall'app di autenticazione o dal metodo configurato per il tuo account | Nella schermata di accesso a GitHub che richiede il codice di autenticazione |
| Codice di autorizzazione del dispositivo, nel formato `XXXX-XXXX` | Dal terminale in cui hai avviato `github-inizio.sh` | Nella pagina "Device Activation" / "Authorize your device" |

**Se il browser copre il terminale:** usa `Alt+Tab` oppure clicca la finestra del terminale nella barra in basso (per esempio `studente@labcalc: ~`). Cerca la riga `First copy your one-time code`, copia il codice e torna al browser. Non chiudere il terminale e non avviare una seconda procedura mentre la prima è in attesa.

**Se il codice del dispositivo è scaduto o la procedura è fallita:** torna al terminale, interrompi l'eventuale attesa con `Ctrl+C` e riesegui `github-inizio.sh`. Usa il nuovo codice mostrato; quello precedente non va riutilizzato.

**Se il browser usa l'account di un altro studente:** esci da quell'account e accedi con il tuo prima di autorizzare. Lo script verifica lo username inserito e, se non corrisponde, rifiuta l'accesso e tenta la pulizia.

### Dal browser al repository personale

3. Apri il link dell'esercitazione fornito dal docente e accedi a [Classroom 50](https://classroom50.org) con **Sign in with GitHub**.
4. Premi **Accept assignment** e attendi la creazione del tuo repository. Poi scegli **Open repository** per aprirlo su GitHub.
5. Nel tuo repository, apri **Code**, seleziona **HTTPS** e copia l'URL.

Il repository creato per te contiene **la tua copia** dell'esercitazione. È questo il repository su cui lavorare: non occorre creare un fork né clonare il template del docente.

### Clonare sul computer

Da un terminale, nella cartella in cui vuoi raccogliere le esercitazioni, esegui i comandi seguenti, sostituendo `URL_COPIATO` con l'URL appena copiato:

```sh
git clone URL_COPIATO
cd esercitazione-0
git remote -v
```

`clone` scarica il repository e la sua cronologia. `origin` è il nome con cui Git identifica il repository remoto: verifica che l'URL mostrato corrisponda al tuo repository nell'organizzazione del corso.

Configura il nome e l'email da associare ai commit di questa copia, sostituendo i valori di esempio con i tuoi:

```sh
git config user.name "Nome Cognome"
git config user.email "email-associata-a-GitHub"
```

Questi dati identificano l'autore dei commit; non sono credenziali di accesso. Esegui i comandi Git dalla cartella `esercitazione-0`, sul branch predefinito che trovi dopo il clone.

Già che ci siamo, configura emacs come editor di default di git

```sh
git config --global core.editor "emacs"
```

o, ancora meglio, emacs da terminale:

```sh
git config --global core.editor "emacs -nw"
```

**Nota Bene:** per salvare e uscire con emacs potete usare la combinazione Ctrl+X Ctrl+S, seguita da Ctrl+X Ctrl+C.

**Checkpoint:** sai aprire il tuo repository su GitHub e riconoscere la copia locale e il suo remoto `origin`.

## Step 1 — Hello World: quale programma ho eseguito?

Prima di modificare `hello.c`, prova a compilarlo (`gcc -o hello hello.c -Wall`) dalla cartella del
repository. Nella sua versione non modificata, il file compila, ma non stampa nulla. 
Completa il TODO in `hello.c` in modo che il programma stampi esattamente:

```text
Hello, computational physics!
```

seguito da una nuova riga.

Dopo aver completato la stampa, Il fatto che il programma compili basta a garantire che faccia ciò che è richiesto?

### Domande stimolo

- Che differenza c'è tra `hello.c` e `hello`? Se modifichi il messaggio nel sorgente e avvii subito l'eseguibile, quale versione stai usando?
- Che cosa cambia quando ricompili?
- Come puoi distinguere ciò che stampa il programma da ciò che mostra il terminale? Che cosa osservi se esegui aggiungendo `> output.txt`?

Scrivi in `osservazioni.md` eventuali osservazioni, e aggiungilo al repository locate e online utilizzando i comandi commit e push (vedi qui sotto). Dopo le prove, ripristina il messaggio richiesto e ricompila.

### Registrare e condividere con Git

- Che differenza c'è fra salvare un file, creare un commit e fare push?
- Quali modifiche mostra `git diff`? Quali file occorrono a un compagno per ricompilare il programma sul proprio computer?
- Come puoi verificare che su GitHub ci sia proprio la versione provata?

I comandi a disposizione sono:

```sh
git status
git diff
git add hello.c osservazioni.md
git diff --staged
git commit -m "Scrivi qui un commento"
git push
git log --oneline -5
```

Sostituisci il messaggio del commit con una breve descrizione delle tue modifiche. `git diff` mostra le modifiche non ancora preparate per il commit; `git diff --staged` mostra quelle selezionate con `git add`. Il commit registra una versione locale, mentre il push la invia a GitHub.

Dopo il push, apri il repository su GitHub e consulta la cronologia dei commit: confronta l'identificativo dell'ultimo commit con quello mostrato da `git log`. Apri anche i file per controllarne il contenuto. Nella prova seguente annoterai questa verifica direttamente su GitHub.

In questa esercitazione i push ordinari condividono gli avanzamenti; la consegna per la valutazione avviene con il tag descritto più avanti.

### Ricevere una modifica da GitHub

Prova ora il percorso inverso. Prima di iniziare, verifica con `git status` di aver registrato e inviato tutte le modifiche locali.

1. Su GitHub apri `osservazioni.md` e usa il pulsante di modifica del file. Aggiungi, nella sezione sul primo step di Git, una frase sulla verifica del commit appena svolta.
2. Registra la modifica con **Commit changes**, scegliendo il branch predefinito del repository e aggiungendo un messaggio appropriato.
3. Prima di cambiare altri file sul computer, apri la copia locale di `osservazioni.md`: la frase è già presente?
4. Dal terminale esegui:

```sh
git status
git pull
git log --oneline -5
```

Riapri il file locale e individua il nuovo commit nella cronologia. `git pull` riceve i nuovi commit dal remoto e aggiorna la copia locale. Perché non è necessario eseguire di nuovo `git clone`? Annota la risposta in `osservazioni.md` e includila nel prossimo commit.

**Checkpoint:** sai compilare, eseguire e spiegare quale versione del programma hai provato e registrato su GitHub.

## Consegna finale

Consegna `hello.c`, `eco.c` e `osservazioni.md` dopo aver completato entrambi
gli step. Non devi caricare separatamente i file: consegni una versione
del repository identificata da un commit.

1. Completa le osservazioni e registra tutte le modifiche con `git add` e    `git commit`, come nello step 1, includendo anche `eco.c`.
2. Esegui `git push`, poi `git status`: non devono rimanere modifiche da registrare o commit da inviare. Controlla su GitHub il commit finale.

### Contrassegnare la versione da consegnare

L'esercitazione usa la modalità di consegna **A tagged commit** di Classroom 50. Un *tag* assegna un nome a un commit: il prefisso `submit/` segnala a Classroom 50 la versione da valutare. Dalla cartella del repository:

```sh
git tag submit/consegna-1
git push origin submit/consegna-1
```

Il primo comando contrassegna il commit corrente; il secondo invia quel tag a GitHub. Il tag non include modifiche non registrate in un commit e il normale `git push` non invia automaticamente questo tag.

Se correggi il lavoro, ripeti verifica, commit e push, poi crea e invia un **nuovo** tag, ad esempio `submit/consegna-2`. Ogni consegna conserva così il riferimento alla propria versione.

### Verificare la consegna

Torna su Classroom 50, apri l'esercitazione e scegli **My submission** per controllare le consegne. Su GitHub verifica che il tag inviato punti al commit finale. Se sono attivi i controlli automatici, segui l'esecuzione nella scheda **Actions** e, quando è terminata, apri **View autograder details** o la pagina **Releases** del repository per leggere il risultato.
Un push riuscito conferma l'invio del lavoro, non il superamento dei test.

Se un test fallisce, leggi il messaggio, correggi il codice e ripeti la consegna con un nuovo tag.
Il superamento dei test non sostituisce la discussione di quello che scrivi in `osservazioni.md`.

Riferimento: [guida ufficiale di Classroom 50 per studenti](https://github.com/foundation50/classroom50/wiki/Web-Student-Guide).
