- **Tipologia:** Strutturale ([[Meta-pattern]] con collegamento di tipo **recursive connection**)
- **Scopo:** Consente di associare nuovi comportamenti agli oggetti inserendoli all'interno di oggetti wrapper speciali che contengono i comportamenti.

> Nella programmazione OOP si tratta di un design pattern che consente di aggiungere il comportamento a un singolo oggetto, staticamente o dinamicamente, senza influenzare il comportamento di altri oggetti della stessa classe. Il pattern Decorator è spesso utile per aderire al principio di [[Conoscenze preliminari#^62f6b3|Single Responsibility]], poiché consente di suddividere la funzionalità tra classi con aree di interesse uniche, nonché al principio [[Conoscenze preliminari#^14625c|Open/Closed]], consentendo di estendere la funzionalità di una classe senza essere modificata.
> - Wikipedia

### Esempio nel mondo reale

Indossare abiti è un esempio dell'utilizzo di decoratori. Quando si ha freddo, ci si avvolge (*wrap*) in un maglione. Se si ha ancora freddo con un maglione, si può indossare una giacca sopra. Se piove magari un impermeabile. Tutti questi abiti *estendono* il comportamento di base ma non fanno parte di una persona e si può facilmente togliere qualsiasi capo di abbigliamento ogni volta che non ce n'è bisogno.

### Anti-pattern con approccio statico e dinamico

Si immagina di voler modellare con degli oggetti una grande varietà, per esempio, di pizze differenti sia per la base (_es. normale, integrale, senza glutine…_) che per gli ingredienti che si trovano sopra. Per ogni diverso tipo di pizza si vorrebbe ottenere un oggetto aderente a un'interfaccia comune `Pizza`, il cui metodo `toString()` elenchi la base e gli ingredienti che la compongono.

Un primo approccio **statico** a questo problema consiste nel creare una gerarchia di classi che contenga una classe per ogni possibile combinazione di base e ingredienti, dette **decorazioni**.

```java
public interface Pizza {}

public class BaseNormale implements Pizza {
    public String toString() { 
        return "Sono una pizza con: base normale"; 
    }
}

public class BaseIntegrale implements Pizza {
    public String toString() { 
        return "Sono una pizza con: base integrale"; 
    }
}

public class BaseNormaleSalame extends BaseNormale {
    public String toString() { 
        return "Sono una pizza con: base normale, salame"; 
    }
}

public class BaseNormaleSalamePeperoni extends BaseNormaleSalame {
    public String toString() {
        return "Sono una pizza con: base normale, salame, peperoni"; 
    }
}

...
```

Si tratta di un **anti-pattern** assolutamente da evitare per diversi motivi:
- **esplosione combinatoria** dovuta all'accoppiamento di ogni possibile base e decorazioni
- una **futura aggiunta** di decorazioni comporterebbe **estrema difficoltà** 

L'ideale sarebbe **poter aggiungere funzionalità e caratteristiche dinamicamente**, restringendo la gerarchia a un'unica classe le cui istanze possano essere *decorate* su richiesta al momento dell'esecuzione.
La soluzione più immediata parrebbe quella definita come [[Anti-pattern God Class|God Class]], cioè un'unica classe in cui attraverso attributi booleani e switch-case vengono attivate/disattivate diverse decorazioni.
Si tratta ovviamente di un altro chiaro **anti-pattern**, sebbene invitante e semplice in prima istanza, nasconde **criticità non trascurabili**:
- viola chiaramente l'[[Conoscenze preliminari#^14625c|Open/Closed Principle]], in quanto per aggiungere un decoratore è necessario modificare la God Class;
- tale classe cresce troppo rapidamente, piena zeppa di funzionalità tra loro molto diverse, con scarsa separazione delle responsabilità (viola il [[Conoscenze preliminari#^62f6b3|Single Responsibility Principle]]), diventando un inferno da leggere, gestire e debuggare in caso di errori.

### Pattern

Si introduce dunque il pattern **Decorator**, la soluzione più universalmente riconosciuta per questo tipo di situazioni.

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/66d161eb9e65c5f8314ad9a2d89c3de5f13730a2.svg)]

A primo impatto l'UML ricorda molto quello del pattern [[Composite]]: si ha un'interfaccia `Component` implementata sia da una classe concreta `BaseComponent` (base della pizza nell'esempio), sia da una **classe astratta** `Decorator`, poi estesa da una serie di decoratori concreti. 

A differenza del Composite però qui ciascun decorator **aggrega un'unica istanza di Component**: questi decorator sono dei *wrapper*, cioè oggetti che **ne ricoprono altri** per aumentare dinamicamente le funzionalità.

Dunque i due diagrammi UML sono molto simili, ma la differenza sta nel **livello di astrazione** in cui ci si pone, infatti le seguenti differenze non si possono cogliere a partire dal solo diagramma UML:

>Nel caso di **Composite** è possibile **creare oggetti composti**, mentre nel **Decorator** si possono **fornire nuove funzionalità dinamicamente**.

Va sottolineato che i **Decorator** ricevono al momento della costruzione, come oggetto da ricoprire, un generico Component, in quanto quest'ultimo permette ai decoratori di decorare oggetti a loro volta già decorati. Si tratta di un approccio **ricorsivo** che permette di creare una catena di decoratori che definisca a **runtime** in modo semplice e pulito oggetti dotati di molte funzionalità aggiunte; così facendo, si alleggerirà la fase di compilazione, aggiungendo funzionalità dinamicamente a runtime.
I decoratori infatti esporranno i metodi definiti dall'interfaccia **delegando** al Component contenuto l'esecuzione del comportamento principale e aggiungendo la propria funzionalità dopo: così la **base** concreta eseguirà il proprio metodo che verrà poi decorato e arricchito dai decoratori in maniera trasparente al client.

```java
public interface Pizza { String toString(); }

public class BaseNormale implements Pizza {
    public String toString() { 
        return "Io sono una pizza con: base normale"; 
    }
}

public class BaseIntegrale implements Pizza {
    public String toString() { 
        return "Io sono una pizza con: base integrale"; 
    }
}

public abstract class IngredienteDecorator implements Pizza {
    private Pizza base;

    public IngredienteDecorator(Pizza base) { this.base = base; }

    public String toString() {
        return base.toString();
    }
}

public class IngredienteSalame extends IngredienteDecorator {
    public IngredienteSalame(Pizza base) { super(base); }

    @Override
    public String toString() { return super.toString() + ", salame"; }
}

public class IngredientePeperoni extends IngredienteDecorator {
    public IngredientePeperoni(Pizza base) { super(base); }

    @Override
    public String toString() { return super.toString() + ", peperoni"; }
}
```

```java
public class Client {
    public static void Main() {
        // Voglio una pizza con salame, peperoni e base integrale
        Pizza salamePeperoni = 
            new IngredientePeperoni(
                new IngredienteSalame(
                    new BaseIntegrale()
                )
            );
    }
}
```

Vista la somiglianza, pattern Decorator e Composite sono facilmente componibili: si può per esempio pensare di creare gruppi di oggetti decorati o decorare in un sol colpo gruppi di oggetti facendo sì che Composite, Decorator e altre classi concrete condividano la stessa interfaccia Component. Un esempio comune ne sono i programmi di photo-editing dove possiamo unire diversi elementi tra loro e applicare a tutti lo stesso effetto.

> [!NOTE] Nota bene
> Al momento della costruzione un Decorator salva al proprio interno l’istanza del Component da decorare. Questo darebbe luogo a un _reference escaping_, ma in questo caso il comportamento è assolutamente voluto: dovendo decorare un oggetto è infatti sensato pensare che a quest’ultimo debba essere lasciata la possibilità di cambiare e che debba essere il decoratore ad adattarsi a tale cambiamento.

È interessante poi osservare la **classe astratta Decorator**: in essa viene infatti inserita tutta la logica di **composizione**, permettendo così di creare nuovi decoratori con estrema facilità. 
Spesso inoltre, se i decoratori condividono una certa parte di funzionalità aggiunte, queste vengono anch’esse estratte nella classe astratta creando un **metodo vuoto protetto** che i decoratori reimplementeranno per attuare la loro funzionalità aggiuntiva.

```java
public abstract class IngredienteDecorator implements Pizza {
    private Pizza base;

    public IngredienteDecorator(Pizza base) { this.base = base; }

    public String toString() {
        return base.toString() + nomeIngrediente();
    }

    protected String nomeIngrediente() { return ""; }
}

public class IngredienteSalame extends IngredienteDecorator {
    public IngredienteSalame(Pizza base) {super(base);}

    @Override
    public String nomeIngrediente() { return ", salame"; }
}

public class IngredientePeperoni extends IngredienteDecorator {
    public IngredientePeperoni(Pizza base) {super(base);}

    @Override
    public String nomeIngrediente() { return ", peperoni"; }
}
```

L'uso della visibilità `protected` rende l’override del metodo possibile anche **al di fuori del package** aumentando così la facilità di aggiunta di nuovi decoratori.
Volendo vedere un esempio concreto di utilizzo di questo pattern è sufficiente guardare alla libreria standard di Java. In essa infatti gli `InputStream` sono realizzati seguendo questo pattern.

#### Beverage modificato rispetto a Head First:
```java
public interface Beverage {
	int cost();
}

public abstract class AbstractCondiment implements Beverage {
	@NotNull private final Beverage beverage;
	public AbstractCondiment(@NotNull Beverage b) { beverage = b; }
	@Override
	public int cost() { return beverage.cost() + condimentCost(); }
	int condimentCost() { return 0 };
}

public class ConcreteCondiment extends AbstractCondiment {
	public ConcreteCondiment(@NotNull Beverage b) { super(b); }
	@Override
	int condimentCost() { return 20; }
}
```


### Pro e Contro

#### Pro
- Puoi estendere il comportamento di un oggetto senza creare una nuova sottoclasse.
- È possibile aggiungere o rimuovere responsabilità da un oggetto in fase di esecuzione.
- Puoi combinare diversi comportamenti wrappando un oggetto in più decoratori.
- [[Conoscenze preliminari#^62f6b3|Single Responsibility Principle]]: È possibile dividere una classe monolitica che implementa molte possibili varianti di comportamento in diverse classi più piccole.

#### Contro
- È difficile rimuovere un wrapper specifico dalla pila di wrapper.
- È difficile implementare un decoratore in modo tale che il suo comportamento non dipenda dall'ordine nello stack dei decoratori.
- Il codice di configurazione iniziale dei livelli potrebbe sembrare piuttosto brutto.


Composite e Decorator hanno diagrammi strutturali simili poiché entrambi si basano sulla **composizione ricorsiva** per organizzare un numero illimitato di oggetti.
Un Decorator è come un Composite ma ha solo un componente figlio. 
**C'è un'altra differenza significativa**: Decorator aggiunge ulteriori responsabilità all'oggetto avvolto, mentre Composite semplicemente *riassume* i risultati dei suoi figli. 
Tuttavia, i pattern possono anche cooperare: puoi usare Decorator per estendere il comportamento di un oggetto specifico nell'albero Composite.

[[Chain of responsibility]] e Decorator hanno diagrammi strutturali molto simili. Entrambi i modelli si basano sulla composizione ricorsiva per passare l'esecuzione attraverso una serie di oggetti. Tuttavia, ci sono diverse differenze cruciali:
- i gestori nel Chain possono eseguire operazioni arbitrarie indipendentemente l'uno dall'altro. Possono anche interrompere l'ulteriore trasmissione della richiesta in qualsiasi momento.
- d'altra parte, vari decoratori possono estendere il comportamento dell'oggetto mantenendolo coerente con l'interfaccia di base. Inoltre, i decoratori non sono autorizzati a interrompere il flusso della richiesta.