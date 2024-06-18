### Storia

Con la diffusione dei primi computer in ambito accademico, negli anni ’50 e ’60 si è subito colta la necessità di superare metodi di produzione “artigianale” del software: sebbene il cliente e il programmatore coincidessero (quindi i problemi di comunicazione e specifiche erano minimi) e i programmi fossero prettamente matematici, si iniziavano a riscontrare i primi problemi. Negli anni ’70 si inizia dunque a pensare a dei metodi, dei processi e a degli strumenti che potessero migliorare e _**“assicurare”**_ la **qualità del software**, sviluppando un approccio di tipo ingegneristico costituito da una serie di fasi.

### Approccio Ingegneristico

1. **Target:** si pone un obiettivo da raggiungere.
2. **Metric:** si definisce una metrica per misurare la [[Qualità del software]], ossia quanto si avvicina al target prefissato. La metrica non va scelta a posteriori.
3. **Method, Process, Tool:** usati per avvicinarsi all'obiettivo
4. **Measurements:** mediante la metrica fissata si misura se le strategie implementative sono state utili e quanto ci hanno avvicinato/allontanato all'obiettivo. In base ai risultati ottenuti, vi sono due possibili strade:
	- **risultati soddisfacenti**: aumento della metrica, dunque accettiamo serenamente i M, P e T usati.
	- **risultati insoddisfacenti:** diminuzione della metrica, dunque ci sono peggioramenti/effetti collaterali, e si vanno modificare delle cose, come target e metrica, ma più comunemente si cambiano i M, P e T usati.
### Target ###

**Obiettivi** da raggiungere:
1. **Risoluzione di problemi** nella [[Progettazione]] del software
2. Assicurarsi di una qualche **[[Qualità del software|qualità]]** che il software dovrà avere
**Domande da porsi:**
- Quali problemi ci sono?
- **Quali qualità deve avere il software?**

### Problemi principali ###

> Una delle più grandi fonti di problemi sono le **persone**.

L'obiettivo della disciplina infatti consiste nel **risolvere problemi di comunicazione**. Essi possono essere tra:
- **il programmatore e il cliente:** esperti di domini diversi, magari il cliente è un gruppo eterogeneo. Inoltre, chi richiede il sw non è detto che lo usi
- **un programmatore e altri programmatori**: stili e conoscenze differenti

Un'altra fonte di problemi sono le **dimensioni del sw**, che possono aumentare considerevolmente (milioni di righe, anni/mesi uomo). Lo sviluppo sw non è più piccolo, generando problemi di **manutenzione e gestione** della codebase.

Il software è **facilmente malleabile** e modificabile nel tempo, ma il moltiplicarsi di versioni, evoluzioni e variazioni di target però possono complicare il lavoro.

> [!Anni uomo? meglio di no]
> La misurazione in *anni uomo* va fatta a posteriori e non prima! Non è buona unità di misura, potrebbe far erroneamente intendere che maggiore è il numero di uomini, minore sarà il tempo speso: non è così.
