# Esercitazione 0 — Compilazione, esecuzione e Git

Riprendiamo la compilazione e l'esecuzione di un programma C, già affrontate
l'anno scorso, e vediamo come ricevere argomenti attraverso `argc` e `argv`.
Useremo **Git** per registrare le versioni del lavoro, **GitHub** per
condividerle con il docente e **Classroom 50** per accettare l'esercitazione
e verificarne la consegna.

Lavora **in locale**, sulla copia del repository assegnato clonata sul tuo
computer. Puoi usare GCC e gli altri strumenti installati sul computer.

## Step 0 — Accettare l'esercitazione e preparare Git

### Dal browser al repository personale

1. Crea un account su [GitHub](https://github.com), se non ne hai già uno,
   e comunica il tuo username al docente per essere inserito nella classe.
2. Accetta l'invito all'organizzazione GitHub del corso.
3. Apri il link dell'esercitazione fornito dal docente e accedi a
   [Classroom 50](https://classroom50.org) con **Sign in with GitHub**.
4. Premi **Accept assignment** e attendi la creazione del tuo repository.
   Poi scegli **Open repository** per aprirlo su GitHub.
5. Nel tuo repository, apri **Code**, seleziona **HTTPS** e copia l'URL.

Il repository creato per te contiene **la tua copia** dell'esercitazione.
È questo il repository su cui lavorare: non occorre creare un fork né
clonare il template del docente.

### Clonare sul computer

Da un terminale, nella cartella in cui vuoi raccogliere le esercitazioni,
esegui i comandi seguenti, sostituendo `URL_COPIATO` con l'URL appena copiato:

```sh
git clone URL_COPIATO
cd esercitazione-0
git remote -v
```

`clone` scarica il repository e la sua cronologia. `origin` è il nome con cui
Git identifica il repository remoto: verifica che l'URL mostrato corrisponda
al tuo repository nell'organizzazione del corso.

Configura il nome e l'email da associare ai commit di questa copia,
sostituendo i valori di esempio con i tuoi:

```sh
git config user.name "Nome Cognome"
git config user.email "email-associata-a-GitHub"
```

Questi dati identificano l'autore dei commit; non sono credenziali di accesso. 
Esegui i comandi Git dalla cartella `esercitazione-0`, sul branch predefinito 
che trovi dopo il clone.

Gia' che ci siamo, configura emacs come editor di default di git

```sh
git config --global core.editor "emacs"
```

o, ancora meglio, emacs da terminale:

```sh
git config --global core.editor "emacs -nw"
```

**Checkpoint:** sai aprire il tuo repository su GitHub e riconoscere la
copia locale e il suo remoto `origin`.

## Step 1 — Hello World: quale programma ho eseguito?

Prima di modificare `hello.c`, esegui `make hello` dalla cartella del
repository (richiede Make e un compilatore C). Il template compila, ma non stampa nulla. 
Completa il TODO in `hello.c` in modo che il programma stampi esattamente:

```text
Hello, computational physics!
```

seguito da una nuova riga.

### Compilazione ed esecuzione

Dalla cartella del repository puoi compilare ed eseguire direttamente:

```sh
gcc -std=c17 -Wall -Wextra -Wpedantic hello.c -o hello
./hello
```

Il `Makefile` fornito permette anche di usare:

```sh
make             # compila hello se il sorgente è cambiato
make clean       # elimina gli eseguibili
```

Dopo aver completato la stampa, Il fatto che il programma compili basta a garantire 
che faccia ciò che è richiesto?

### Domande stimolo

- Che differenza c'è tra `hello.c` e `hello`? Se modifichi il messaggio nel
  sorgente e avvii subito l'eseguibile, quale versione stai usando?
- Che cosa cambia quando ricompili?
- Come puoi distinguere ciò che stampa il programma da ciò che mostra il
  terminale? Che cosa osservi se esegui aggiungendo `> output.txt`?

Scrivi in `osservazioni.md` eventuali osservazioni. 
Dopo le prove, ripristina il messaggio richiesto e ricompila.

### Registrare e condividere con Git

- Che differenza c'è fra salvare un file, creare un commit e fare push?
- Quali modifiche mostra `git diff`? Quali file occorrono a un compagno per
  ricompilare il programma sul proprio computer?
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

Sostituisci il messaggio del commit con una breve descrizione delle tue
modifiche. `git diff` mostra le modifiche non ancora preparate per il commit;
`git diff --staged` mostra quelle selezionate con `git add`. Il commit
registra una versione locale, mentre il push la invia a GitHub.

Dopo il push, apri il repository su GitHub e consulta la cronologia dei
commit: confronta l'identificativo dell'ultimo commit con quello mostrato
da `git log`. Apri anche i file per controllarne il contenuto. Nella prova
seguente annoterai questa verifica direttamente su GitHub.

Gli eseguibili sono ignorati da Git: si ricostruiscono dal sorgente. 
In questa esercitazione i push ordinari condividono gli avanzamenti;
la consegna per la valutazione avviene con il tag descritto più avanti.

### Ricevere una modifica da GitHub

Prova ora il percorso inverso. Prima di iniziare, verifica con `git status`
di aver registrato e inviato tutte le modifiche locali.

1. Su GitHub apri `osservazioni.md` e usa il pulsante di modifica del file.
   Aggiungi, nella sezione sul primo step di Git, una frase sulla verifica
   del commit appena svolta.
2. Registra la modifica con **Commit changes**, scegliendo il branch
   predefinito del repository.
3. Prima di cambiare altri file sul computer, apri la copia locale di
   `osservazioni.md`: la frase è già presente?
4. Dal terminale esegui:

```sh
git status
git pull
git log --oneline -5
```

Riapri il file locale e individua il nuovo commit nella cronologia.
`git pull` riceve i nuovi commit dal remoto e aggiorna la copia locale.
Perché non è necessario eseguire di nuovo `git clone`? Annota la risposta
in `osservazioni.md` e includila nel prossimo commit.

**Checkpoint:** sai compilare, eseguire e spiegare quale versione del
programma hai provato e registrato su GitHub. Discuti una tua prova con il
docente, poi passa allo [step 2 — Eco degli argomenti](step-2.md), nello
stesso repository.

Nello step 2, oltre alle prove proposte, individua `argc` e `argv` in `eco.c`:
perché il programma richiede `argc == 4` pur ricevendo tre argomenti?
Che cosa contiene `argv[0]`? Annota le risposte in `osservazioni.md`.

## Consegna finale

Consegna `hello.c`, `eco.c` e `osservazioni.md` dopo aver completato entrambi
gli step. Non devi caricare separatamente i file: consegni una versione
del repository identificata da un commit.

1. Completa le osservazioni e registra tutte le modifiche con `git add` e
   `git commit`, come nello step 1, includendo anche `eco.c`.
2. Esegui `git push`, poi `git status`: non devono rimanere modifiche da
   registrare o commit da inviare. Controlla su GitHub il commit finale.

### Contrassegnare la versione da consegnare

L'esercitazione usa la modalità di consegna **A tagged commit** di
Classroom 50. Un *tag* assegna un nome a un commit: il prefisso `submit/`
segnala a Classroom 50 la versione da valutare. Dalla cartella del repository:

```sh
git tag submit/consegna-1
git push origin submit/consegna-1
```

Il primo comando contrassegna il commit corrente; il secondo invia quel tag
a GitHub. Il tag non include modifiche non registrate in un commit e il
normale `git push` non invia automaticamente questo tag.

Se correggi il lavoro, ripeti verifica, commit e push, poi crea e invia un
**nuovo** tag, ad esempio `submit/consegna-2`. Ogni consegna conserva così
il riferimento alla propria versione.

### Verificare la consegna

Torna su Classroom 50, apri l'esercitazione e scegli **My submission** per
controllare le consegne. Su GitHub verifica che il tag inviato punti al
commit finale. Se sono attivi i controlli automatici, segui l'esecuzione
nella scheda **Actions** e, quando è terminata, apri **View autograder details**
o la pagina **Releases** del repository per leggere il risultato.
Un push riuscito conferma l'invio del lavoro, non il superamento dei test.

Se un test fallisce, leggi il messaggio, correggi il codice e ripeti la consegna con un nuovo tag.
Il superamento dei test non sostituisce la discussione delle prove raccolte in `osservazioni.md`.

Riferimento: [guida ufficiale di Classroom 50 per studenti](https://github.com/foundation50/classroom50/wiki/Web-Student-Guide).