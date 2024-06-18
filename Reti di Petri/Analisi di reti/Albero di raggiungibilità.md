Per generare l'**albero di raggiungibilità** di una **rete di Petri** si può applicare il seguente **algoritmo**:

01    **crea la radice** corrispondente alla marcatura iniziale $M_0$, etichetta il nodo come **nuovo**; 
02    **==finché== esistono nodi etichettati come "nuovo"** esegui:
03        **seleziona** una marcatura $M$ con etichetta **"nuovo"** e **rimuovi l'etichetta**.
04        **==se==** la **$M$ è identica** a una marcatura sul cammino dalla radice a $M$ allora:
05            **etichetta** $M$ come **"duplicata"**;
06            **==continua==** alla prossima iterazione.
07        **==se==** **nessuna transizione** è **abilitata** in $M$ allora:
08            **etichetta** la marcatura come **"finale"**;
09            situazione di deadlock.
10        **==finché== esistono transizioni abilitate in $M$** esegui per ognuna di esse:
11            **crea la marcatura $M'$** prodotta dallo **scatto di $t$** (cioè *fai scattare $t$*);
12            **crea un nuovo nodo** corrispondente a $M'$;
13            **aggiungi un arco** nell'albero da $M$ a $M'$;
14            **etichetta la marcatura $M'$** come **"nuovo"**.

(Nota a margine: nodo *alias* di marcatura)

### Esempio

Di seguito è mostrata una consegna di un esercizio riguardo gli alberi di raggiungibilità.

> Modellare tramite una rete di Petri l’accesso ad una risorsa condivisa tra quattro lettori e due scrittori, ricordandosi che i lettori possono accedere contemporaneamente, mentre gli scrittori necessitano di un accesso esclusivo.

Come primo approccio, si possono creare **due reti**, una per i **lettori** e una per gli **scrittori**. Si può successivamente procedere modellando la **risorsa** condivisa collegando le diverse parti create.

![Esempio albero di raggiungibilità](https://marcobuster.github.io/sweng/assets/15_esempio-1-albero-raggiungibilita.png)

Essendo presente un solo gettone nel posto _Risorsa_, i **lettori** non sono in grado di accedervi contemporaneamente. Per risolvere questo problema, si può aumentare il numero di gettoni all’interno di _Risorsa_ a 4. Per evitare che gli scrittori possano accedere alla _Risorsa_ mentre viene letta, è possibile aggiungere un peso pari a 4 sugli archi da “_Risorsa”_ a _“S_inizia”_ e da _“S_finisce”_ a _“Risorsa”_.

Così facendo, per accedere alla _Risorsa_ uno **scrittore** dovrà attendere che tutti i token saranno depositati in essa, garantendo che nessun’altro sta utilizzando la risorsa (funge da *lock*).

Il **risultato finale** è il seguente:

![[Rete esempio in raggiungibilità.png]]

### Costruzione albero di raggiungibilità

Una volta creata la rete finale, è possibile **generare** l’albero di raggiungibilità seguendo l’**algoritmo precedente**.

**Marcatura**: LettoriPronti | LettoriAttivi | Risorsa | ScrittoriPronti | Scrittori Attivi

Il primo passo è creare il **nodo radice** corrispondente alla marcatura iniziale e marcarlo come **nuovo**: `40420`.

Successivamente, occorre procedere **per ogni nodo marcato come "nuovo"**. In questo caso l’unico nodo marcato come _nuovo_ è `40420`. Dopo aver rimosso l’etichetta _nuovo_ si verifica che, partendo dalla radice dell’albero, non siano già presenti altri nodi uguali. Essendo `40420` esso stesso la radice (e unico nodo dell’albero), si procede.

A questo punto, **per ogni transizione abilitata nella marcatura** presa in considerazione (`40420`) la si fa **scattare** generando le altre marcature e marcandole come _nuovo_ (`40011` e `31320`) che quindi si **collegano** con un arco alla marcatura originale (`40420`).

La situazione attuale è la seguente:

![Esempio albero primo giro algoritmo](https://marcobuster.github.io/sweng/assets/15_esempio-1-albero-prima-giro-algoritmo.png)

Si procede quindi con l’algoritmo ripetendo i passi fino ad arrivare in una situazione in cui **non esistono più nodi nuovi**, marcando nel mentre come duplicati tutti i nodi che si re-incontrano, in quanto già presenti almeno una volta nell’albero.

La **situazione finale** sarà la seguente:

![Esempio albero finale](https://marcobuster.github.io/sweng/assets/15_esempio-1-albero-finale.png)

L’albero di raggiungibilità sopra in figura è ora **completo** e rappresenta tutti gli _stati_ raggiungibili.

Grazie a questo albero, se si volesse verificare che gli scrittori sono in **mutua esclusione** con i lettori, basterà controllare se non esiste una marcatura in cui il secondo e il quinto numero (rispettivamente _“LettoriAttivi”_ e _“ScrittoriAttivi”_) sono entrambi contemporaneamente maggiori di zero. Si può verificare in modo esaustivo (*model checking*) guardando tutti i nodi dell’albero. 

Inoltre si può verificare se gli **scrittori** si **escludono a vicenda**, controllando se in ogni marcatura l’ultimo numero (_“ScrittoriAttivi”_) non è maggiore di uno. Si può infine verificare l’assenza di **deadlock**, data dalla presenza o meno di nodi terminali.

Collassando i nodi aventi la stessa marcatura, si può verificare dall’albero di raggiungibilità se la rete è **viva**.

![Esempio di grafo di raggiungibilità](https://marcobuster.github.io/sweng/assets/15_grafo-di-raggiungibilita.png)

La rete è anche **[[Stato base e rete reversibile|reversibile]]** in quanto ogni stato è uno **stato base** ed è quindi possibile raggiungere da ogni stato tutti gli altri stati.  
Avendo questo grafo si vede che la rete è **[[Vitalità di una transizione#^638d35|viva]]**, in quanto sono rappresentate tutte le transizioni all’interno del grafo, e siccome il sistema è **reversibile** è sempre possibile riportarsi ad una situazione in cui si può far scattare una transizione.


### Limiti

- Per poter creare un albero di raggiungibilità è necessario enumerare tutte le possibili marcature raggiungibili, di conseguenza **la rete deve essere obbligatoriamente limitata**: non sarebbe altrimenti possibile elencare tutti i nodi.
- la **crescita** (esponenziale) del numero degli stati globali può risultare velocemente **ingestibile** per una rete limitata.
- Questa tecnica di analisi **non è in grado di rilevare se una rete è limitata** o meno. Nel caso in cui si sappia già che la rete è limitata, l’albero di raggiungibilità non perde informazioni ed è l'esplicitazione degli stati della rete (quindi ne è di fatto la FSM corrispondente).