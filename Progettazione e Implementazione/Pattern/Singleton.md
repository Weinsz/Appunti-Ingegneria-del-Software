- **Tipologia:** Creazionale
- **Scopo:** Permette di garantire che una classe abbia una sola istanza, fornendo comunque punto d’accesso globale a quest’istanza

> Nell'ingegneria del software, il pattern Singleton limita l'istanza di una classe a un unico oggetto. Ciò è utile quando è necessario esattamente un oggetto per coordinare le azioni nel sistema.
> - Wikipedia


Si vorrebbe che di un determinato oggetto esista **un'unica istanza**, in quanto logicamente l'esistenza di più copie di quest'ultimo non avrebbero senso (es. più istanze della classe `Game` quando c'è un solo gioco alla volta nel sistema). Però nei linguaggi OOP le classi possono essere istanziate senza limiti più volte, perciò la realizzazione di quest'unicità è più complessa.

La soluzione data dal pattern **Singleton** (tipologia di [[Meta-pattern]] **unification**) consiste nel rendere la classe stessa **responsabile** del fatto che non ci debba essere più un'istanza. Per far ciò, bisogna prima rendere **non pubblico** il costruttore (meglio *protected* così da creare sottotipi).
Bisogna però garantire comunque un modo per recuperare l’unica istanza disponibile della classe: si crea dunque il _metodo statico_ `getInstance` che restituisce a chi lo chiama l’unica istanza della classe, creandola tramite il costruttore privato se questa non è già presente. Tale istanza è infatti memorizzata in un _attributo statico_ e privato della classe stessa, in modo da poterla restituire a chiunque ne abbia bisogno.

La creazione dell'istanza unica avviene solo alla prima chiamata del metodo statico per non appesantire il carico della JVM. Risulta inutile istanziare un oggetto non necessario, ma è meglio farlo quando viene richiesto.
[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/b010048de788581e97c2a12c09ec06c8ca87902d.svg)]

Tuttavia non vi è la certezza di non creare più di un’istanza di sé stessa, perché non viene considerata la **concorrenza**. Se due processi accedono in modo concorrente al metodo `getInstance`, per problemi di scheduling, entrambi potrebbero eseguire il controllo sul valore nullo dell’istanza nello stesso momento (prima che l’altro processo lo abbia effettivamente istanziato) e quindi rischiare di creare più di un oggetto, o addirittura causare la restituzione di un valore nullo, poiché non ancora istanziata effettivamente!

Una prima soluzione a questo problema potrebbe essere quella di mettere un lock sull’esecuzione del metodo anteponendovi la direttiva `@Synchronized`: tuttavia, tale approccio comporterebbe un notevole calo di prestazioni in quanto verrà usata ogni volta che chiamerò il metodo e non solo alla prima chiamata.  

Una soluzione molto più efficiente è invece quella che prevede l’utilizzo del pattern concorrente **Double check**, che viene implementato in modo da avere un _blocco sincronizzato_ di istruzioni posto all’interno del ramo if in cui si verifica effettivamente che l’istanza sia nulla, e solo allora si esegue il costruttore in maniera *synchronized*.
La presenza del doppio controllo assicura che non vi siano squilibri dovuti alla concorrenza, mentre sincronizzare solamente un blocco e non l’intero metodo fa sì che il calo di prestazioni sia presente solamente durante le prime chiamate concorrenti.

Questa soluzione non era applicabile prima di Java 5 poiché al tempo l’allocazione della memoria di un oggetto e l’effettiva creazione dell’istanza erano gestite separatamente, quindi c’era il rischio di avere solo allocato la memoria ma senza averci scritto nulla, quindi sarebbe stato possibile restituire un riferimento a una porzione di memoria vuota. Da Java 5 l’allocazione e la creazione dell’oggetto sono state “_accorpate_” in una singola operazione a livello di JVM e quindi il problema non si pone più.

```java
public class Singleton {
    private static Singleton instance = null;
    
    protected Singleton() {}
    
    public static Singleton getInstance() {
        if (instance == null) {
            synchronized(Singleton.class) {
                if (instance == null)
                    instance = new Singleton();
            }
        }
        return instance;
    }
    public void sampleOp() {...}
}
```

### Idioma Java

Ogni linguaggio ha i propri idiomi per i vari pattern. Nel caso di Java, il Singleton invece che essere implementato mediante classe, si sfrutta l'enumerativo con un unico valore, vale a dire l'**istanza**. Ciascun valore di tali oggetti è trattato nativamente come Singleton: viene creato al momento del suo primo uso, ce n'è solo una copia, si accede sempre alla stessa istanza. In più, l'`enum` permette di aggiungere attributi e metodi.

```java
public enum Singleton {
    INSTANCE;

    public void metodoIstanza() { ... }
}

Singleton.INSTANCE.sampleOp();
```

Approccio thread-safe, gestito nativamente da Java.

> [!NOTE] Joshua Bloch, Effective Java 2nd Edition p.18:
>  Un tipo enum con elemento singolo è il modo migliore per implementare un singleton

### Contro

Si tratta di un pattern utile e interessante, ma va usato con cautela in quanto potrebbe vìolare alcuni [[Conoscenze preliminari#^0a9782|principi SOLID]]. Più informazioni a riguardo [qui](https://www.davidtanzer.net/david%27s%20blog/2016/03/14/6-reasons-why-you-should-avoid-singletons.html).

- Viola il principio [[Conoscenze preliminari#^62f6b3|Single Responsibility]], poiché il pattern risolve due problemi alla volta.
- Il vero problema con Singleton è che dà una buona scusa per non pensare attentamente alla visibilità appropriata di un oggetto. Trovare il giusto equilibrio tra esposizione e protezione per un oggetto è fondamentale per mantenere la flessibilità.
- Potrebbe essere difficile fare unit testing del codice client di Singleton perché molti framework di test si basano sull'ereditarietà durante la produzione di oggetti mock. Poiché il costruttore della classe singleton è privato e l'override dei metodi statici è impossibile in Java, si dovrà pensare a un modo creativo per fingere il singleton. O semplicemente non utilizzare il pattern Singleton.