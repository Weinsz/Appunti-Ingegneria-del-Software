### Di cosa si occupano

Gli [[Software Configuration Management|SCM]] non dipendono da linguaggi di programmazione, infatti questi lavorano su file, considerandone le righe di testo. Ignorando quindi se sia codice, un immagine o altri formati, gli SCM considereranno questi come un insieme di linee testuali. Un’eccezione è Monticello, che consiste in un intero ambiente di sviluppo per il linguaggio Smalltalk, contenente un tool di versioning creato appositamente per questo linguaggio.

Ogni **cambiamento** è regolato da:
- **check-out**: dichiara la volontà di lavorare partendo da una particolare revisione di un manufatto (o di una configurazione di diversi manufatti);
- **check-in** (o **commit**): dichiara la volontà di registrarne una nuova (spesso chiamata **change-set**).

Queste operazioni vengono attivate rispetto a un **repository**. Lo scambio di dati è tra il repository (che contiene tutte le configurazioni) e il workspace (l’ambiente in cui si trova nel filesystem).
Solitamente ho **1 repository e n workspace**, uno per ogni ambiente dove sto lavorando.

### Repository

La repo mantiene date, etichette, versioni, diramazioni (**branches**) e altri dati. Per risparmiare spazio, le repository salvano solo le differenze tra una versione e l’altra. In realtà [[Git]] non fa così, perché usa **link simbolici:** fare il **checkout** di una specifica versione è istantaneo.

Le repository possono essere **centralizzate** o **distribuite**.

Nei sistemi di versioning distribuiti c’è il concetto di **hashing**, in modo da identificare file uguali anche se in **posizioni diverse**. Per confrontare storie diverse si utilizzano gli hash dei file e delle directory.

#### Cosa tracciare in un progetto?

Sicuramente devono essere tracciati tutti i file relativi al codice sorgente o file di configurazione, ma per quanto riguarda il resto non c’è una risposta precisa, perché dipende dalle necessità; in linea di massima però occorre prendere due decisioni importanti che influenzano la **replicabilità** della produzione, ovvero:

- si traccia l’evoluzione dei componenti fuori dal nostro controllo (come ad esempio compilatori o librerie)?
- si archiviano i file che costituiscono il prodotto (ovvero file generati come i file i binari)?

Solitamente la risposta a queste due domande è **no**, questo perché tracciare le librerie o i binari del software è costoso e poco pratico, ma così facendo **la perfetta replicabilità va perduta**. 
Infatti è possibile che alcuni sw con il passare del tempo non possano essere eseguiti perché le tecnologie necessarie al loro funzionamento non sono più disponibili (compilatori con una versione molto vecchia ad esempio). 
C’è da dire però che, se un progetto viene mantenuto costantemente, la sua vita viene allungata di conseguenza. A volte può avere senso versionare dei file generati, infatti è possibile distribuire le diverse versioni tramite _"package"_. Su alcuni siti come GitHub o GitLab ci sono delle sezioni (diverse da quelle dove viene messo il codice) dedicate alla pubblicazione di questi package, ma questo non è un vero e proprio versioning come viene fatto per il codice tramite git (non vi è una storia modificabile, ma solo una serie di versioni del software).

### Accesso concorrente

Quando il repository è condiviso da un gruppo di lavoro, **nasce il problema di gestirne l’accesso concorrente**. Esistono due modelli:
- **modello _pessimistico_** (RCS): si prevede il possibile conflitto assicurandosi che chi lavora sia l’unico con l’accesso in scrittura. Funziona solo in **ambienti centralizzati**, nell’open source non può funzionare.
- **modello _ottimistico_** (CVS): il sistema si disinteressa del problema e fornisce supporto per le attività di _merge_ di **change-set paralleli** potenzialmente conflittuali.

Il modello ottimistico può essere regolato con i branch: l’attività di _merge_ è quindi fondamentale. CVS/Subversion scoraggiava i branch, mentre [[Git]] li rende facili e li incoraggia. In Git, l’uso dei branch è talmente comune che a volte è necessario introdurre delle politiche (come [[GitFlow]]) sul loro utilizzo.

### SCM distribuito: centralizzato vs decentralizzato

Il mondo **open source preferisce un approccio decentralizzato** al version control. Perché?

Sfruttare i sistemi di SCM in modo distribuito può portare diversi vantaggi a fronte di alcune problematiche. I vantaggi sono diversi, tra cui:
- è possibile lavorare **offline**, e una volta che si ha a disposizione una connessione internet sarà possibile aggiornare il repository remoto;
- è molto più **veloce**, perché non c'è la rete di mezzo che avrebbe potuto fare da bottleneck;
- supporta più modi di lavorare:
	- **simil-centralizzato**: si ha un repo **di riferimento** raggiungibile da tutti;
	- **due peer** che collaborano direttamente, condividendo tra loro il proprio lavoro;
	- **gerarchico** a più livelli (kernel Linux).

La problematica principale di questo approccio è che ogni peer ha un suo repository e **non vi è una sincronizzazione automatica**, di conseguenza sono necessari dei comandi espliciti per fare il _merge_ ad un altro repository. 

(In git, per via della sua **struttura modulare**, è possibile usare il proprio algoritmo di merge rispetto a quelli già presenti.)