- **Tipologia:** Comportamentale ([[Meta-pattern]] con recursive connection)
- **Scopo:** Consente di passare le richieste lungo una catena di gestori. Dopo aver ricevuto una richiesta, ogni gestore decide di elaborare la richiesta o di passarla al gestore successivo nella catena.

Si ha dunque un _client_ in grado di fare una richiesta, e una **catena di potenziali gestori** di cui non sappiamo a priori chi sarà in grado di gestirla effettivamente.

Ci sono infatti dei casi in cui si vorrebbe definire una gestione “a cascata” di una certa richiesta. 
Si pensi per esempio a una serie di regole anti-spam: all’arrivo di una mail, la prima regola la esamina e si chiede se sia applicabile o meno; in caso affermativo contrassegna la mail come spam, altrimenti _la passa alla prossima regola_, che a sua volta farà lo stesso test passando il controllo alla terza in caso negativo, e così via. 

Un **anti-pattern** comune è quello di creare una serie di _if-then-else_ per gestire ogni caso in successione. Ciò porterebbe ad avere un codice estremamente illeggibile, confusionario e non mantenibile nel caso in cui si debbano aggiungere nuove _regole_ di controllo. L'obiettivo dunque è quello di **separare ogni caso**, per renderli più leggibili e mantenibili, semplificando anche la trasmissione della responsabilità da un caso al successivo.

Il pattern **Chain of Responsibility** risolve il disaccoppiamento tra client e gestore **concatenando i gestori**. Esso prescrive la creazione di un’interfaccia a cui tutti i gestori devono aderire, contenente solo la dichiarazione di un metodo `evaluate` che implementa la logica descritta prima: si stabilisce se si può gestire la richiesta, e in caso contrario si chiama lo stesso metodo su _un altro gestore_, corrispondente a un riferimento di un altro oggetto del tipo dell'interfaccia, ottenuto come parametro al momento della creazione e corrispondente al suo successore nella catena.

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/8364b7bfbf5feb849e5ca3e70bd9f57965698ed1.svg)]

In questo modo all’interno del client è sufficiente creare una vera e propria catena di gestori e chiamare il metodo `evaluate` del primo. L’ordine in cui vengono assemblati tali gestori conta, in quanto la valutazione procede sequenzialmente.

```java
public interface Handler {

    /* Il tipo di ritorno dipende dal campo applicativo */
    public ??? evaluate(); 

}

public class Client {

    private Handler evaluator = 
        new ConcreteHandler1(
            new ConcreteHandler2(
                new ConcreteHandler3(null)));

    public void richiesta() {
        evaluator.evaluate();
    }

}

public class ConcreteHandler implements Handler {

    private final Handler next;

    public ConcreteHandler(Handler next) {
        this.next = next; //next potrebbe anche essere null
    }

    public ??? evaluate() {
        if canHandle() return "Questo evaluatore gestisce il caso";
        else if next != null return next.evaluate(); //provo con il successivo
        else return "Non sono in grado di gestire questo caso";
		//sono arrivato all'ultimo caso e non sono stato in grado di gestirlo
    }

}

```

L'aggregazione tra `ChainedHandEvaluator` e sé stesso rappresenta la **catena** nel design pattern Chain of Responsibility. 
L'aggregazione è indicata da una freccia con un diamante all'estremità della freccia che punta all'interfaccia `ChainedHandEvaluator`. La notazione "0..1" indica che un oggetto `ChainedHandEvaluator` può avere zero o un successore.

I valutatori dovranno avere un costruttore in grado di ricevere **null**, o in alternativa bisogna avere un modo per gestire il caso in cui si si cerchi di chiamare il metodo `evaluate` su un oggetto `null`. Per fare ciò è possibile sollevare un’eccezione, ma il modo migliore sarà quello di sfruttare il [[Null Object]] pattern per creare una **strategia di default** da utilizzare come **terminatore**.

```java
// Esempio Carte Poker
public interface ChainedHandEvaluator {
	// Null Object come strategia di default
    ChainedHandEvaluator HIGH_RANK = pokerHand -> HandRank.HIGH_CARD;
    
    @NotNull HandRank handEvaluator(@NotNull PokerHand pokerHand);
}

public class TrisEvaluator implements ChainedHandEvaluator {
    private final ChainedHandEvaluator next;
    
    public TrisEvaluator(ChainedHandEvaluator evaluator) {
        next = evaluator;
    }
    
    @Override
    public @NotNull HandRank handEvaluator(@NotNull PokerHand pokerHand) {
        if (isTris(pokerHand))
            return HandRank.THREE_OF_A_KIND;
        else
            return next.handEvaluator(pokerHand);
    }
    
    private boolean isTris(PokerHand pokerHand) {
        Map<Rank, Integer> occ = new EnumMap<>(Rank.class);
        for(Card c : pokerHand) {
            int num = occ.getOrDefault(c.getRank(), 0);
            if (num == 2)
                return true;
            else
                occ.put(c.getRank(), num + 1);
        }
        return false;
    }
}
```

- **Perché l'aggregazione si fa da interfaccia a interfaccia e non da classe a interfaccia?**

L'aggregazione si fa **da interfaccia a interfaccia** invece che da **classe a interfaccia** per garantire la massima **flessibilità** e **disaccoppiamento**. Questo permette a qualsiasi classe che implementa l'interfaccia di essere parte della catena di responsabilità.

Se l'aggregazione fosse fatta da classe a interfaccia, ciò limiterebbe la flessibilità del design pattern. Le classi specifiche potrebbero avere requisiti o comportamenti specifici che non sono applicabili o desiderabili per altre classi nella catena. Inoltre, l'uso di classi specifiche potrebbe introdurre **dipendenze indesiderate**.

Utilizzando interfacce, si può garantire che ogni elemento della catena rispetti un contratto comune, pur mantenendo la sua indipendenza. Questo rende il design pattern Chain of Responsibility estremamente versatile e riutilizzabile.


Il pattern Chain of Responsibility può essere implementato in vari modi e l'aggregazione con cardinalità "0..1" è solo uno di questi. Alcuni altri modi includono:
1. **Aggregazione con cardinalità "1..1"**: in questo caso, ogni elemento della catena deve avere un successore. Questo significa che l'ultimo elemento della catena deve riferirsi a se stesso o a un elemento di default che può gestire tutte le richieste rimanenti. **Avrei però una catena infinita.**
2. **Aggregazione con cardinalità "0.._"(o "1.._")**: in questo caso, ogni elemento della catena può avere più successori. Questo può essere utile se si desidera implementare una sorta di *"tree of responsibility"* in cui una richiesta può essere gestita da più di un elemento della catena.
3. **Aggregazione suddivisa**: un altro modo sarebbe stato avere una classe concreta che implementa l'interfaccia Handler e non ha il campo next, e un'altra gerarchia di nodi della catena che hanno un riferimento next all'interfaccia Handler (dunque devono averne esattamente 1), ma si tratta di una situazione più libera, forse più di quella che vorremmo.
4. **Senza aggregazione**: invece di utilizzare l'aggregazione, si potrebbe utilizzare un "handler" centrale che mantiene una lista di tutti gli elementi della catena e li itera fino a trovare uno che può gestire la richiesta. Questo è meno comune e può essere più difficile da gestire, ma può essere utile in alcuni casi.

### Pro vs Contro

#### Pro
- Puoi controllare l'ordine di gestione delle richieste.
- [[Conoscenze preliminari#^62f6b3|Single Responsibility Principle]]: È possibile disaccoppiare le classi che richiamano operazioni dalle classi che eseguono le operazioni.
- [[Conoscenze preliminari#^14625c|Open/Closed Principle]]: Puoi introdurre nuovi gestori nell'app senza violare il codice client esistente.

#### Contro
Alcune richieste potrebbero non essere gestite.