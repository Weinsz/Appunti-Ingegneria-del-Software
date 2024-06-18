- **Tipologia:** Creazionale
- **Scopo:** Fornisce un'interfaccia per la creazione di oggetti in una superclasse, ma permette alle sottoclassi di modificare il tipo di oggetti che verranno istanziati. Delega di fatto la logica di istanziamento alle sottoclassi.

> Nella programmazione OOP, è un pattern creazionale che utilizza i metodi factory per affrontare il problema della creazione di oggetti senza dover specificare la classe esatta dell'oggetto che verrà creato. Questo viene fatto creando oggetti mediante la chiamata di un metodo factory, specificato in un'interfaccia e implementato da classi figlie, o implementato in una classe base e facoltativamente sovrascritto da classi derivate, piuttosto che chiamando un costruttore.
> - Wikipedia

## Problema

Immagina di creare un'applicazione per la gestione della logistica. All'inizio può gestire solo il trasporto su camion, quindi la maggior parte del codice risiede all'interno della classe `Truck`.

Dopo un po', l'app diventa piuttosto popolare e ogni giorno si ricevono dozzine di richieste da compagnie di trasporto marittimo per incorporare la logistica marittima nell'app. Ottima notizia, vero? Ma per quanto riguarda il codice? L'aggiunta di una nuova classe al programma non è così semplice se il resto del codice è già accoppiato a classi esistenti. Infatti al momento, la maggior parte del codice è accoppiata alla classe `Truck`. L'aggiunta di navi `Ships` nell'app richiederebbe modifiche all'intera codebase.

Inoltre, se in seguito si decide di aggiungere un altro tipo di trasporto all'app, probabilmente si dovranno apportare nuovamente tutte queste modifiche. Di conseguenza, ci si ritrova con un codice brutto, pieno di condizioni che cambiano il comportamento dell'app a seconda della classe degli oggetti di trasporto.

### Pattern

Spesso capita che un certo client sia interessato a creare un oggetto non in base al suo tipo quanto all’_interfaccia_ che esso implementa. Al client non importa conoscere la classe di cui l’oggetto è istanza perché questo non ha alcuna rilevanza nel suo contesto. Tuttavia, la normale creazione di un oggetto tramite la keyword `new` richiede di esplicitare la classe a cui esso appartiene, costringendo così il client ad approfondire inutilmente la sua conoscenza sui tipi che implementano l’interfaccia a cui è interessato.

Per evitare questo tipo di situazione si introduce uno dei cosiddetti **pattern creazionali**: stiamo parlando del pattern dei **Factory Method**. 
Esso definisce una classe astratta `Creator` dotata di **metodi di fabbricazione** *astratti* che restituiscono un’istanza di un tipo aderente all’interfaccia ``Product`` a cui il client è interessato: a quale classe appartenga effettivamente tale istanza (cioè quale **Product concreto**) è però lasciato ad un **Creator concreto** tra i tanti che estendono la classe astratta; idealmente dovrebbe esserci un creatore concreto per ogni tipo di prodotto concreto che implementa l’interfaccia Product.

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/efd1937047900b7977adb4e32f72e63f2a6e34eb.svg)]

Questo pattern definisce dunque un’**interfaccia per creare un Product ma delega al Creator concreto la scelta di cosa creare effettivamente**: in questo modo all’interno della classe astratta Creator è possibile scrivere dei metodi che richiedono la creazione di un Product pur senza sapere di preciso il tipo dell’oggetto che verrà creato, in quanto questo sarà determinato dall’implementazione di `factoryMethod()` del creatore concreto. 
Si sfruttano dunque al massimo grado **polimorfismo** e **collegamento dinamico**, in quanto il tipo dell’oggetto da creare viene deciso a runtime: poiché nemmeno il Creator conosce il tipo concreto dei Product creati risulta dunque subito chiaro perché i factory method non possano essere metodi statici di tale classe, in quanto non sarebbe associato all'oggetto e non avremmo dunque polimorfismo e collegamento dinamico.
I factory methods rappresentano un esempio dell’utilità delle astrazioni permesse dai linguaggi ad oggetti: in un contesto in cui normalmente non è possibile fare overriding, come un costruttore, la soluzione è quella di virtualizzare il tutto con la creazione di metodi che possono essere esportati in classi concrete. Per questo motivo i factory method vengono talvolta detti anche _virtual constructors_, “costruttori virtuali”.

### Esempio

Per capire meglio il funzionamento del pattern, vediamo un esempio di come esso può essere utilizzato. Consideriamo un software capace di aprire contemporaneamente più documenti di tipo differente in diverse pagine, come per esempio Microsoft Word o Excel: al loro interno, quando viene creato un nuovo file vengono fatte una serie di operazioni generiche (creare la nuova pagina, mostrare vari popup…), ma ad un certo punto è necessario creare un oggetto che rappresenti il nuovo documento e il cui tipo dipende dunque dal documento creato. 
Il codice di creazione del nuovo oggetto `Document` non può dunque trovarsi in un metodo della classe astratta `Application` (il Creator) insieme con il resto delle operazioni generiche, in quanto specifico della tipologia di documento creato. 
Dunque è necessario virtualizzare la creazione dell’oggetto in un metodo `createDocument()` implementato da una serie di sottoclassi concrete `MyApplication` (Concrete Creator) ciascuna specifica per un tipo di documento.
[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/5e46fc80df9745acb24fc455c0b57eb2c6e7a476.svg)]

### Pro e Contro

#### Pro
- Evita l'accoppiamento stretto tra il creatore e i prodotti concreti.
- [[Conoscenze preliminari#^62f6b3|Single Responsibility Principle]]: Puoi spostare il codice di creazione del prodotto in un punto del programma, semplificando il supporto del codice.
- [[Conoscenze preliminari#^14625c|Open/Closed Principle]]: È possibile introdurre nuovi tipi di prodotti nel programma senza violare il codice client esistente.

#### Contro
- Il codice potrebbe diventare più complicato poiché è necessario introdurre molte nuove sottoclassi per implementare il pattern. Lo scenario migliore è quando stai introducendo il pattern in una gerarchia esistente di classi Creator.