Si tratta del processo che seguiamo per costruire, consegnare, installare ed evolvere il prodotto software, dall'idea fino alla consegna e al ritiro finale del sistema.

Ci sono diverse problematiche:
- I **requisiti** imposti dal cliente possono cambiare spesso.
- Produrre sw **non riguarda solo lo scrivere codice**
- Bisogna risolvere i **problemi di comunicazione** tra le varie parti (dev, progettista e dev, ecc.).
- Bisogna essere **rigorosi**. Pro e contro: può facilitare la comprensione di ciò che bisogna fare ma implica maggior fatica e viceversa.

> [!NOTE] Ipotesi di Bauer Zemanek
> Metodi formali riducono in maniera significativa gli errori di progettazione, o permettono di eliminarli e risolverli prima.

- Si tratta di un'ipotesi in quanto non si può dimostrare, tuttavia nella pratica ciò avviene costantemente. Prima si trovano gli errori nella fase di sviluppo, più sarà facile risolverlo. Non è sempre necessario però usare metodi formali, richiedendo molto tempo da sottrarre ad altre fasi. Spesso le consegne imminenti non permettono l'investimento nella formalità.
- Ci sono tanti **aspetti** da considerare e da affrontare uno per volta. Per parlarne ho bisogno di metodi di comunicazione diversi, che riguardano ruoli diversi in tempi diversi: **Aspect Oriented Programming**.

Tenendo conto di questi problemi è necessario decidere come organizzare l'attività di sviluppo sw in modo da evitarli. Per modellare un ciclo di vita del sw occorre dunque prima **identificare le varie attività necessarie**, decidendone le precedenze temporali e chi le debba fare.

Ci si pone due domande:
1. Cosa devo fare ora?
2. Fino a quando? Come?

L'[[Approccio Ingegneristico|ingegneria del sw]] prova a rispondere a queste domande.
Inizialmente nell'ambito dello sviluppo sw è stato usato il modello **code and fix**. Dopo poco si è rivelato estremamente inefficace in gruppi di lavoro complessi, generando codice poco leggibile e mantenibile, specie quando il cliente non era più lo sviluppatore stesso ma utenti/clienti con poco know-how.

Per ovviare a ciò i sw engineers hanno individuato diverse **fasi del ciclo di vita di un sw**, che combinate, potessero produrre sw di qualità.

## Fasi del ciclo di vita del sw

### Studio di fattibilità

L'attività svolta per decidere se il processo di sviluppo dovrebbe iniziare.
**Obiettivo**: produrre un **documento in linguaggio naturale** (perché diretto a manager) presentante diversi scenari di sviluppo con soluzioni alternative, con una discussione sui trade-off tra benefici e costi attesi. 
In dettaglio, esso include:
- uno studio di diversi scenari di realizzazione, scegliendo:
	- le architetture e hw necessario;
	- se sviluppare da sé o subappaltare ad altri.
- stima dei costi, tempi di sviluppo, risorse necessarie, benefici delle alternative e valutazione del **return on investment**.
Spesso l'analisi viene delegata esternamente per risparmiare tempo e/o costi.
### Analisi e specifica dei requisiti

Attività più critica e fondamentale del processo di produzione del sw.
**Obiettivo**: stesura di un **documento di specifica**.

In questa fase i **progettisti** devono:
- comprendere il **dominio applicativo** del prodotto, dialogando con il cliente e la controparte tecnica
- identificare gli **stakeholders** e studiarne le richieste. Spesso non sono figure omogenee e le loro necessità differiscono
- capire quali sono le **funzionalità richieste**: la domanda più importante che deve porsi il programmatore è il **cosa, non il come**. Al cliente non interessano giustamente gli aspetti tecnici. Le **specifiche** vanno dunque viste dal punto di vista del cliente
- stabilire un **dizionario comune** tra cliente e sviluppatore che può anche far parte della specifica, per evitare ambiguità e disguidi
- definire **altre qualità** che possono essere richieste dal cliente: esempio, _"La centrale non deve esplodere"_ non è un dettaglio implementativo, ma un **requisito** detto **non** **funzionale**, in quanto queste ulteriori qualità non sempre sono solo esterne.

Dunque c'è un duplice obiettivo: deve essere approvato dagli stakeholders per soddisfare il cliente, ed è usato dai programmatori per sviluppare una soluzione che soddisfi le sue aspettative, fungendo da punto di partenza per il design. 
Essendo un documento contrattuale va scritto in modo formale.

Deve essere presente anche un **piano di test**, ovvero una collezione di collaudi che certificano la correttezza del lavoro: se questi test hanno esito positivo il lavoro viene pagato, altrimenti non viene accettato. Nell'ingegneria del sw è molto complesso collaudare tutti i casi e stati possibili.

Un altro output è il **manuale utente** o **maschere d'interazione**, cioè la vista esterna del sistema da progettare.

Si possono sfruttare due tipi di modelli per produrre il documento di specifica:
- **Modelli descrittivi:** rappresentano il sistema logicamente in modo da poter verificare le sue proprietà
- **Modelli operazionali:** forniscono una rappresentazione del sistema tramite un modello eseguibile capace di mostrare le proprietà del sistema; non bisogna però pensare al come realizzare una funzionalità

> [!NOTE] Legge di David
> Il valore dei modelli che rappresentano il sw da diversi punti di vista dipendono dal POV assunto, ma non c'è nessuna vista che è la migliore per ogni scopo.
### Progettazione (Design)
Attività attraverso cui gli sviluppatori strutturano l'applicazione.
**Obiettivo**: scrivere un **documento di specifica di progetto** contenente la descrizione architetturale del sw.
Durante questa fase occorre quindi:
- scegliere un'architettura sw di riferimento
- **scomporre** in moduli o oggetti i compiti e ruoli: **object oriented design**
- **identificare [[Design Pattern]]**
### Programmazione e test di unità
**Obiettivo**: avere un **insieme di moduli** separati **sviluppati indipendentemente** con un’interfaccia concordata e **singolarmente verificati**.

**Black boxes**: gli oggetti o moduli del punto precedente vengono realizzati, definendo per ciascuno **test unitari** che mostrano la **correttezza.** Il testing non va fatto infatti alla fine di tutto.

I singoli moduli si testano indipendentemente, anche se alcune funzioni da cui dipendono non ci sono ancora (**stub**). Altri moduli **driver** forniscono invece una situazione su cui applicare il modulo sotto test.
### Integrazione e test di sistema
Si integrano insieme i moduli singolarmente implementati e testati. In alcuni modelli di sviluppo 
(**[[Modelli incrementali]]**) viene accorpata alla fase prima.
I moduli stub e driver vengono sostituiti coi componenti reali.
Ovviamente si aggiunge incrementalmente un modulo alla volta, per prevenire errori.
Fondamentale poi testare l'intero programma (**test d'integrazione**).
Integrazione con approccio *top down* o *bottom up*.
**Fase** **finale**: **alpha testing**, in condizioni realistiche
### Consegna, installazione e manutenzione
**Output:** prodotto migliore.
- Il sw va poi **consegnato** ai clienti, prima però si seleziona utenti nella fase di **beta testing**.
- L'**installazione** (*deployment*) definisce il runtime fisico dell'architettura del sistema
- La **manutenzione** può essere definita come l'insieme delle attività finalizzate a modificare il sistema dopo la consegna al cliente. La manutenzione può essere di tipo::
	- **correttivo**: sistemare errori nel sistema
	- **adattivo**: adattare il sw ai nuovi requisiti (**evolvibilità**)
	- **perfettivo**: migliorare aspetti interni senza modificare quelli esterni, potendo però subire miglioramenti e riducendo il debito tecnico
Necessario sviluppare avendo in mente la futura manutenzione di ciò che si sta scrivendo: il **costo della manutenzione** incide nel costo del sw in misura spesso oltre il 60%.

### Altre attività

- **Documentazione**: vista alcune volte come **attività trasversale** da creare seguendo l'evoluzione del progetto. Attività spesso procrastinata in quanto **le specifiche possono cambiare frequentemente**. Vi sono delle figure in alcuni gruppi che se ne occupano, ma può essere pericoloso, in quanto non tutti possono capire l'opera di uno sviluppatore
- **Verifica e controllo qualità**: la verifica quasi sempre si attua mediante [[Tecniche di review|review]] e [[Software inspection|ispezioni]] del codice. Si vuole anticipare il prima possibile la scoperta e risoluzione degli errori per non consegnare prodotti difettosi. Attività da fare con costanza e **non tutta alla fine**
- **Gestione processo**: gestione incentivi con premi di produzione, responsabilità, formazione, perferzionamento del processo, ecc.
- **Gestione configurazioni**: gestione delle relazioni e risorse di sviluppo inter-progettuali.
  **Es.** una libreria condivisa tra più progetti, che vorrebbero modificarla




processi di sviluppo

processo di sviluppo