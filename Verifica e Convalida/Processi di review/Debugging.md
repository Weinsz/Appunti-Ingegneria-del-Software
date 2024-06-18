Il **debugging** è l'insieme di tecniche che mira a **localizzare** e **rimuovere** le *anomalie* che sono le cause dei *malfunzionamenti* riscontrati nel programma. 
> Come già accennato, il debugging **non deve** essere usato per rilevare tali malfunzionamenti.

Il debugging richiede una **comprensione approfondita del codice** e del funzionamento del programma e può essere un processo complesso e articolato.
Tuttavia, può contribuire in modo significativo a migliorare la **qualità** e la **stabilità** del codice, oltre a **risolvere malfunzionamenti**.

Trattandosi di ricerca delle anomalie che generano malfunzionamenti noti, l'attività è definita per un **programma** e un **insieme di dati** che *causano* malfunzionamenti. Essa si basa infatti sulla **riproducibilità del malfunzionamento**, verificando prima che non sia dovuto in realtà a **specifiche errate**. 

Si tratta di un’**attività molto complicata**, come fa notare Brian W. Kernighan nella sua famosa citazione:
> “Il debugging è il doppio più difficile che scrivere il codice in primo luogo. Pertanto, se scrivi il codice nel modo più intelligente possibile, non sei, per definizione, abbastanza intelligente per debuggarlo”.

Dunque è importante **scrivere codice più semplice possibile** in modo da poterne fare un altrettanto **semplice debugging** dove necessario.


### Perché è così difficile?

L'attività di debugging è particolarmente complessa soprattutto perché:
- non è sempre facile individuare con precisione la **relazione anomalia-malfunzionamento**: non è un legame banale, in quanto potrebbero esserci anomalie che prima di manifestarsi sotto forma di malfunzionamenti abbiano avuto **molte evoluzioni**.
- **non esiste una relazione biunivoca** tra anomalie e malfunzionamento: non è detto che un'anomalia causi un unico malfunzionamento, e nemmeno che quest'ultimo sia causato da una sola anomalia.

Un altro problema è dovuto al fatto che la **correzione di anomalie** non garantisce per niente un software migliore o con meno errori: per correggere un'anomalia è necessario per forza di cose anche **modificare il codice**, ma ogni volta che viene fatto si apre la possibilità di introdurre **nuove anomalie nello stesso codice**.

> 10 little Indian boys went out to dine;
> One choked his little self and then there were 9.
> 
> 9 little Indian boys sat up very late;
> One overslept himself and then there were 8.
> 
> 10 little bugs were in the code.
> Take one down, patch it around.
> **27 little bugs were in the code…**


### Tecnica naïve

La tecnica di debugging più utilizzata dai dev consiste nell'introdurre nel modulo in esame una serie di **comandi di output** (es. *print*) che stampino su console il valore intermedio assunto dalle sue variabili. Questo permetterebbe di osservare l'evoluzione dei dati e, si spera, di comprendere la causa del malfunzionamento a partire da questa storia.

Nonostante sia **facile da applicare** (bastano un compilatore e un esecutore), si tratta in realtà di una tecnica **molto debole**: non solo essa **richiede la modifica del codice** e quindi una rimozione di tali modifiche una volta individuata l'anomalia, ma è **poco flessibile** in quanto richiede una nuova modifica e compilazione per ogni stato esaminato.

Bisogna inoltre considerare che questa tecnica testa un **programma diverso** dall'originale, presentando *print* aggiuntive solo **apparentemente innocue** e senza effetti collaterali.

L'unico scenario (irrealistico) in cui la tecnica potrebbe essere **considerata sufficiente** sarebbe nel caso in cui il codice sia progettato così bene e il modulo così ben isolato che basterebbe un'unica *print* per **risalire all'anomalia**.

#### Tecnica naïve “avanzata”

Un miglioramento parziale alla tecnica naïve appena descritta si può ottenere sfruttando le **funzionalità del linguaggio** (oppure alcuni **tool specifici** per il debug), come per esempio:
- `#ifdef` per variabile di debug e `gcc -D` per il linguaggio C;
- **librerie di logging** (con diverso livello, es. *warning, info, debug...*), che permettono peraltro di rimuovere i messaggi di log in fase di produzione del codice;
- **asserzioni**, ovvero check interni al codice di specifiche proprietà: possono essere visti anche come **“oracoli” interni** al codice che permettono di segnalare facilmente stati illegali.

Ciò non toglie che la tecnica sia comunque **naïve**, in quanto si sta ancora modificando il codice in modo che fornisca informazioni aggiuntive.


### Dump di memoria

Una tecnica leggermente più interessante è quella dei **dump di memoria**, che consiste nel produrre un'**immagine esatta della memoria del programma** dopo un passo d'esecuzione: si scrive cioè su un file l'intero contenuto della memoria a livello di linguaggio macchina (_nei sistemi a 32 bit, la dimensione dei dump può arrivare fino a 4GB_).
Viene (veniva) fatta come analisi *post-mortem*, cioè quando il programma crashava prima di terminare e distruggersi diceva:
```txt
Segmentation fault (core dumped)
```

- `Segmentation fault`: trovato qualcosa che non va, problema nei segmenti di memoria;
- `core dumped`: ti ho scritto sul disco tutto quello che c'era in memoria, con successivo remove core dump, essendo troppe informazioni e impossibile da guardare bene.

Sebbene questa tecnica non richieda la **modifica del codice**, essa è spesso **difficile da applicare** a causa della differenza tra la **rappresentazione astratta** dello stato (legata alle strutture dati del linguaggio utilizzato) e la **rappresentazione a livello di memoria** di tale stato. Viene inoltre prodotta un'**enorme mole di dati** per la maggior parte **inutili**.


### Debugging simbolico

Il prossimo passo è invece il cosiddetto **debugging simbolico**, un’attività che utilizza **tool di debugging** specifici per **semplificare la ricerca delle anomalie** che causano il malfunzionamento in esame.
Tali strumenti permettono di **osservare in tempo reale l’esecuzione del programma**, rendendo possibile analizzare l’**evoluzione** del valore delle variabili passo per passo: questi tool **non alterano il codice** ma **come** esso viene eseguito.

A tal proposito, i **debugger simbolici** forniscono informazioni sullo stato delle variabili usando lo stesso dominio d'astrazione del linguaggio usato per scrivere il codice: gli stati sono cioè rappresentati con gli **stessi simboli** e stesse strutture dati, rendendo quindi **utile** l'attività d'**ispezione dello stato**.

Essi poi forniscono **ulteriori strumenti** che permettono di *visualizzare* il comportamento del programma in **maniera selettiva**, come per esempio _**watch**_ e _**spy monitor**_.

Per regolare il **flusso del programma** è poi possibile inserire **breakpoint** e **watchpoint** su certe linee di codice che ne **arrestino l’esecuzione** in uno specifico punto, eventualmente rendendoli dipendenti dal valore delle variabili. Volendo poi **riprendere l’esecuzione** si può invece scegliere la **granularità** del passo successivo:
- **singolo**: si procede alla linea successiva;
- **dentro una funzione**: si salta al codice eseguito dalle funzioni chiamate sulla riga corrente;
- **drop/reset del frame**: vengono scartate le variabili locali nel frame d’esecuzione della funzione, ritornando ad una situazione precedente.

#### Debugging per prova

Avendo questo continuo monitoraggio degli stati, molti tool di debugging simbolico permettono non solo la visualizzazione ma anche l'**esame automatico degli stati ottenuti**, in modo da verificarne la **correttezza**.

Soprattutto, utilizzando **watch condizionali** si possono aggiungere **asserzioni a livello di monitor**, verificando così che certe **proprietà** continuino a valere durante l’**intera esecuzione**. Così, per esempio, è possibile chiedere al **_monitor_** (cioè l’**_esecutore_** del programma) di controllare che gli *indici di un array* siano sempre interni all’intervallo di definizione.


#### Altre funzionalità del debugger

Non finisce qui: i **debugger moderni** sono strumenti veramente molto interessanti, che permettono per esempio anche di:
- **modificare il contenuto di una variabile** (o zona di memoria) a *runtime*;
- **modificare il codice**: nonostante non sia sempre possibile e necessita ricompilazione, poi si prosegue dal punto in cui ci si era interrotti; può essere comodo per esempio dopo tante iterazioni di un ciclo;
- **ottenere rappresentazioni grafiche dei dati**: strutture **dinamiche** come *puntatori, alberi e grafi* possono essere rappresentate graficamente per migliorare la comprensione dello stato.
  Un esempio è per IntelliJ col debugger degli **Stream** e la loro pipeline:
```java
public static void main(String[] args) {
	Day01 d = new Day01();
	
	System.out.println(d.inputAsScanner()
	.useDelimiter("\n\n").tokens()
	.map(s -> new Scanner(s)
	.tokens()
	.mapToLong(Long::parseLong)
	.sum())
	.sorted(Comparator.reverseOrder())
	.limit(3)
	.mapToLong(Long::valueOf)
	.sum()
	);
}
```


### Il debugging può essere automatizzato?

Parlando di testing si è sempre parlato di **testing automatico** (non manuale), cioè credibile e ripetibile. Per il **debugging** invece? Una volta riparato l'errore non lo si vuole ripetere, dunque c'è da automatizzare la parte iniziale, vale a dire la scoperta; quindi si vuole **automatizzare le operazioni di debugging** che si fanno mentalmente per individuare l'anomalia.

Andreas Zeller tratta questo argomento in maniera approfondita nel suo [Debugging Book](http://debuggingbook.org/), proponendo alcune direzioni di sviluppo di **ipotetici strumenti di debugging automatico**.

I due concetti principali della trattazione sono i seguenti:
- **shrinking input**: dato un **input molto grande** e complesso che causa un **malfunzionamento**, degli strumenti automatici possono aiutare a **ridurre** il più possibile l'input in modo da semplificare il debugging;
- **differential debugging**: dato lo stesso input, in maniera automatica vengono **esplorati gli stati** del programma **mutando ad ogni iterazione piccole porzioni di codice** per individuare dove è più probabile che si trovi l’anomalia.

Purtroppo per il momento la prospettiva di debugger automatici **è ancora lontana**.  
Tuttavia, esiste già qualcosa di simile, vale a dire il comando **`git bisect`** di Git: data una versione vecchia in cui il bug non è presente, una versione nuova in cui esso si è manifestato e un oracolo che stabilisce se il bug è presente o meno, Git esegue una **ricerca dicotomica** per trovare la versione che ha introdotto il problema. 
Sebbene non sia proprio la stessa cosa, si tratta sicuramente di uno strumento utile.