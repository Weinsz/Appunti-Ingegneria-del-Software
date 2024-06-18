- **Tipologia:** Strutturale ([[Meta-pattern]] con collegamento di tipo **recursive connection**)
- **Scopo:** Consente di comporre oggetti in strutture ad albero e quindi lavorare con queste strutture come se fossero **singoli oggetti**, trattandoli in modo uniforme

> Nell'ingegneria del software, il pattern Composite è un design pattern strutturale di partizionamento. Consiste nel fatto che un gruppo di oggetti deve essere trattato allo stesso modo di una singola istanza di un oggetto. L'intento è quello di _comporre_ oggetti in strutture ad albero per rappresentare gerarchie part-everything. L'implementazione del pattern consente ai client di trattare i singoli oggetti e le composizioni in modo uniforme.
> - Wikipedia

Si immagini di dover modellare un **file system** in un'applicazione: esso sarà composto di File e Directory, le quali dovranno essere in grado di contenere al loro interno ulteriori file e directory.
Si dovrà quindi ottenere una **struttura ad albero** di Directory, avente dei file come **foglie**.
Se però molte funzionalità del file system operano in modo analogo sia su file che directory (es. *creazione, cancellazione, ottenimento dimensione, ecc.*), come si può gestire queste due classi in modo uniforme, in modo da evitare duplicazione del codice?

Per gestire simili strutture ad albero che rappresentano _insiemi e gerarchie di parti_ viene introdotto il pattern **Composite**, che mira a gestire oggetti singoli, gruppi, gruppi di gruppi, in maniera uniforme e trasparente così che un client non interessato alla struttura gerarchica possa usarli senza accorgersi delle differenze.

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/dd7cd8b658aa3c1cf7cbccca59d60306a0cd0ed6.svg)]

Si hanno quindi gli oggetti singoli concreti, rappresentati dalla classe `Leaf`, e gli oggetti composti rappresentati dalla classe `Composite`. Per realizzare l’**uniformità di gestione** dobbiamo introdurre un livello di astrazione, quindi **Leaf e Composite implementano una stessa interfaccia Component** contenente la definizione delle operazioni comuni.

L’uso dell’interfaccia comune permette di definire all’interno di Composite le operazioni di aggiunta e rimozione di oggetti al gruppo in modo generale, permettendo cioè che un **Composite aggreghi sia Leaf che altri Composite**.

A proposito di tale **aggregazione**, dallo schema UML possiamo notare le relative cardinalità (_recursive connection_ dei meta-pattern): **"0..n" dal lato del Composite e "0..1" da quello del Component**. 
Esse indicano che:
- **Un'istanza di Composite aggrega 0 o più istanze di Component al suo interno**: così è possibile che al momento della creazione, il Composite sia vuoto; se ciò non ha senso logico nel programma, si può mettere "1..n" imponendo il passaggio di un Component al costruttore;
- **Un'istanza di Component può essere contenuta in al più un'istanza di Composite**: può così esistere da solo oppure può essere aggregato in un gruppo, ma non può appartenere contemporaneamente a più gruppi, cosa che **forza una struttura strettamente ad albero**.

Nella maggior parte dei casi un'istanza Composite userà gli oggetti aggregati per implementare effettivamente i metodi descritti dall'interfaccia comune, delegando ad essi l'esecuzione effettiva e limitandosi a elaborare i risultati. Riprendendo l’esempio di prima, per conoscere la dimensione di una Directory sarà sufficiente sommare le dimensioni dei file e delle altre directory in essa contenuti.

### Pro e Contro

Il pattern Composite presenta numerosi vantaggi, ma non è nemmeno esente da criticità:
- Puoi lavorare con strutture ad albero complesse in modo più conveniente: usa il polimorfismo e la ricorsione a tuo vantaggio.
- [[Conoscenze preliminari#^14625c|Open/Closed Principle]]: puoi introdurre nuovi tipi di elementi nell'applicazione senza rompere il codice esistente, che ora funziona con l'albero degli oggetti.
- Potrebbe essere difficile fornire un'interfaccia comune per le classi la cui funzionalità differisce troppo. In alcuni scenari, dovresti generalizzare eccessivamente l'interfaccia del componente, rendendola più difficile da comprendere.
- L’uso di un’**interfaccia comune** per Leaf e Composite permette al client di non preoccuparsi del tipo dell’oggetto con cui sta interagendo, in quanto ogni Component è in grado di eseguire le operazioni descritte nell’interfaccia in modo indistinguibile; tuttavia, questo implica che **non è possibile distinguere** tra oggetti singoli e composti.
- L’uso dell’interfaccia non rende possibile imporre l’aggregazione solo di specifici elementi.

In realtà vi sono delle differenze tra le foglie e i Composite, infatti quest’ultimi possono essere considerati come una Leaf con qualche peculiarità in più, come ad esempio la possibilità di aggiungere o rimuovere degli elementi dal gruppo. Questo quindi definisce una differenza tra le due classi, ma a questo punto si pone un problema dal punto di vista dell’utente:
#### Come si può capire se un Component è una Leaf o un Composite? 

Ci sono diverse possibilità, come ad esempio inserire un metodo apposito nell’interfaccia che ritorna un oggetto Composite, e in base all’implementazione deve essere tornato this oppure null. 

È facilmente intuibile però che questa soluzione non è buona, infatti un miglioramento è quello di utilizzare un **casting controllato** (altrimenti si riscontrerebbero dei problemi), in cui prima di eseguire il casting si effettua un controllo sfruttando il costrutto `instanceOf` di Java. 
In alternativa è possibile **spostare tutte le operazioni nell’interfaccia**, sollevando un’eccezione quando queste vengono chiamate da un oggetto Leaf.

Queste due soluzioni sono entrambe "sporche", infatti facendo ciò si sta cercando di differenziare degli elementi che per definizione del pattern devono essere indistinguibili.

### Esempio Composite con CardSource e Deck

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/53417eb13fb698d787ba339d2745b1b362fff260.svg)]

Applicando questo pattern al caso del deck, possiamo modellare un mazzo generico in modo che sia formato internamente da deck o da altri gruppi di deck; in questo modo è possibile creare oggetti più complessi a partire da degli oggetti base (Deck).

Il codice della classe che rappresenta il deck composto sarebbe la seguente:
```java
public class CompositeCardSource implements CardSource {
    @NotNull private List<CardSource> sources;
    public boolean isEmpty() {
        for(CardSource source : sources)
            if(!source.isEmpty()) return false;
        return true;
    }
} 
```

Il metodo `isEmpty` restituirà true se e solo se tutti i `CardSource` che contiene saranno vuoti. 
Utilizzando questa implementazione però il `draw` viene reso meno banale, perché per simulare un’estrazione di una carta è necessario almeno pescarla da un mazzo scelto casualmente. 

Quindi ci sono dei compromessi da rispettare se si sceglie di adottare il pattern, accettando tutti i pro e i contro.

**Composite e [[Decorator]] hanno diagrammi di struttura simili** poiché entrambi si basano sulla composizione ricorsiva per organizzare un numero illimitato di oggetti.
Un **Decorator** è come un Composite ma ha **solo un componente figlio**. C'è un'altra differenza significativa: Decorator aggiunge ulteriori responsabilità all'oggetto avvolto, mentre Composite semplicemente “riassume” i risultati dei suoi figli. Tuttavia, i pattern possono anche cooperare: puoi usare Decorator per estendere il comportamento di un oggetto specifico nell'albero Composite.