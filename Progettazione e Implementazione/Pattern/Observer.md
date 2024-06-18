- **Tipologia:** Comportamentale
- **Scopo:** Consente di definire un meccanismo di sottoscrizione per notificare a più oggetti eventuali eventi che si verificano all'oggetto che stanno osservando. In sostanza, ci si registra come osservatore per ricevere i cambiamenti di stato nell'oggetto.

> Observer è un design pattern in cui un oggetto, chiamato **subject**, mantiene un elenco dei suoi dipendenti, chiamati **observers**, e li notifica automaticamente di qualsiasi cambiamento di stato, solitamente chiamando uno dei loro metodi.
> - Wikipedia

### Problema

Si immagini di avere due tipi di oggetti: un `Cliente` e un `Negozio`. Il cliente è molto interessato a una particolare marca di prodotto che dovrebbe essere disponibile nel negozio molto presto. Il cliente può visitare il negozio tutti i giorni e verificare la disponibilità dei prodotti. Ma mentre il prodotto è ancora in viaggio si sprecherebbe tempo d'altronde.

D'altra parte, il negozio potrebbe inviare tante e-mail (che potrebbero essere considerate spam) a tutti i clienti ogni volta che diventa disponibile un nuovo prodotto. Ciò salverebbe alcuni clienti da viaggi infiniti al negozio. Allo stesso tempo, sconvolgerebbe altri clienti che non sono interessati ai nuovi prodotti.
Sembra ci sia un conflitto: o il cliente perde tempo a controllare la disponibilità del prodotto o il negozio spreca risorse avvisando i clienti sbagliati. Meglio fare una newsletter con l'iscrizione delle persone interessate.

### Esempio nel mondo reale

Se ci si abboni a un quotidiano o ad una rivista, non serve più recarsi in negozio per verificare se è disponibile il prossimo numero. Invece, l’editore invia i nuovi numeri direttamente alla casella di posta personale subito dopo la pubblicazione, o anche in anticipo. L'editore mantiene un elenco di abbonati e sa a quali riviste sono interessati. Gli abbonati possono lasciare l'elenco in qualsiasi momento se non più interessati.


### Pattern

Spesso capita di avere nei programmi una serie di elementi che vanno tenuti sincronizzati, esempio una palette di colori che deve aggiornare i valori RGB in base a ciò che seleziona l'utente col mouse. Abbiamo cioè uno **stato comune** che va mantenuto coerente in tutti gli elementi che lo manipolano.

Nella realizzazione di questa struttura si rischia di cadere nell'**anti-pattern delle pairwise dependencies**, in cui ogni vista dello stato deve conoscere tutte le altre. 
Ciò significa che tra le varie classi vi è un **forte accoppiamento e una bassissima espandibilità**, in quanto per aggiungere una vista dobbiamo modificare tutte le altre (violo [[Conoscenze preliminari#^14625c|Open/Closed Principle]]). Basta avere poco più di 2 viste diverse perché il numero di dipendenze cresca esponenzialmente (quindi anche di errori); inoltre questo anti-pattern viola totalmente il *principio di separazione* 
([[Conoscenze preliminari#^62f6b3|Single Responsibility Principle]]), che sottolinea **forte coesione interna e pochi accoppiamenti esterni**.

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/9bdbe64b8d7fd9dcca665bb053172ce001543dc2.svg)]

La soluzione proposta dal pattern **Observer** è dunque quella di estrarre la parte comune, cioè lo **stato**, e isolarlo in un oggetto a parte detto **Subject**: questo oggetto verrà osservato da ogni vista, le cui classi prendono ora il nome di **Observer**. Così si sta quindi **centralizzando la gestione dello stato**, dunque saranno presenti diverse classi che osserveranno una classe centrale e reagiranno a ogni cambiamento di stato di quest'ultima.
Si tratta una situazione talmente comune che in Java sono presenti delle classi (ora deprecate in quanto non _thread-safe_) per realizzare questo pattern: `java.util.Observer/Observable`.

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/b208e369d953f4c2f62de785d0af543dc92871a6.svg)]

#### Come fanno gli Observer a sapere che il Subject è cambiato?

L’idea di fare un continuo _polling_ (chiedere “sei cambiato?” al Subject), non è ovviamente sensata, in quanto sarebbe dipendente dal tempo che passa tra una richiesta e l’altra, di conseguenza esiste il rischio di una risposta troppo lenta oppure un eccessivo utilizzo di risorse.

La soluzione è invece quella di **invertire la responsabilità** con un’**architettura event-driven**: gli Observer si **registrano al Subject**, che li informerà al suo cambiamento di stato.

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/b6b58adff998d29456a52cebe9aef62a17da6890.svg)]

#### Come si collegano Observer e Subject?

Come si vede in figura, esiste una classe `Observable` che funge da base da cui ereditare per ogni Subject; vi è poi un’interfaccia `Observer` che gli Observer concreti devono ovviamente implementare.

A questo punto gli Observer si possono sottoscrivere al Subject semplicemente attraverso l’uso delle sue funzioni `addObserver()` e `removeObserver()`, venendo così sostanzialmente inseriti o rimossi nella lista interna degli Observer interessati.
Una volta che lo stato del Subject viene cambiato, solitamente attraverso una serie di metodi pubblici che permettano a tutti di modificarlo (`setState()`), esso chiama dunque il suo metodo `notifyObservers()`: questo non fa altro che ciclare su tutti gli Observer sottoscritti chiamandone il metodo `update(Observable, Object)`. In questo metodo:
- `Observable` è il Subject di cui è stato modificato lo stato. L’uso di interfacce permette di sottoscrivere un Observer a più Subject tra cui disambiguare al momento dell’update.
- `Object` è la parte di stato che è cambiata (_Object_ perché il tipo dipende ovviamente dal Subject in questione).

Sul metodo di **notifica del cambiamento di stato** esistono però due diverse filosofie, **push** e **pull**, ciascuna con i suoi campi applicativi prediletti, andando a evidenziare quando e come esse vengono usate.


### Push

In questo caso l’argomento Observable nell'`update` viene messo nullo, mentre **nell’Object viene passata la totalità dello stato** del Subject:
```java
// Observable
@Override
public void notifyObservers() {
    for (Observer observer : observers) {
        observer.update(null, state);
    }
}

// Observer
@Override
public void update(Observable model, Object state) {
    if (state instanceof Integer intValue) {
        doSomethingOn(intValue);
    }
}
```

Come si vede, dovendo definire come reagire al cambiamento di stato, in `update` l’Observer dovrà innanzitutto fare un down-casting per ottenere un oggetto della classe corretta. Avendo la responsabilità di tale casting, **l’Observer dovrà conoscere precisamente la struttura dello stato del Subject**, creando una **forte dipendenza** che potrebbe creare problemi di manutenibilità.

Un altro problema di questo approccio è che gli Observer sono solitamente interessati a una **piccola porzione dello stato del Subject**, quindi passarlo tutto come parametro potrebbe **sovraccaricare la memoria** inutilmente.


### Pull

^89e961

Con questo approccio, invece di mandare lo stato all’`update`, **viene passato il Subject stesso**, il quale conterrà uno o più metodi per accedere allo stato (`getState()`):
```java
// Observable
@Override
public void notifyObservers() {
    for (Observer observer : observers) {
        observer.update(this, null);
    }
}

// Observer
@Override
public void update(Observable model, Object state) {
    if (model instanceof ConcreteObservable cModel) {
        doSomethingOn(cModel.getState());
    }
}
```

Sebbene comporti un passaggio in più poiché **l’Observer deve chiamare un metodo del Subject quando riceve la notifica**, questo cambio di prospettiva offre due vantaggi: 
1. non viene passato tutto lo stato, il che fa risparmiare molta memoria; il Subject potrebbe decidere di rendere disponibili sottoinsiemi diversi dello stato con getter diversi, mostrando così ad ogni Observer solo le informazioni per esso rilevanti.
2. sebbene anche in questo caso sia richiesto un casting (da Observable a Subject), questo approccio rende meno dipendenti dalla rappresentazione interna del Subject, in quanto fintantoché **la firma dei getter non cambia** lo stato interno del Setter può cambiare senza problemi.

### Approccio ibrido e dipendenze

Spesso nei casi reali gli approcci _push_ e _pull_ sono **ibridati** tra di loro: ad `update` viene passato sia il Subject che quella parte di stato utile a tutti gli Observer, mentre qualora gli serva qualcosa di più specifico essi se lo andranno a prendere con il *getter*.

Il vero **problema di entrambi gli approcci** è però quello delle **dipendenze**:
- nella modalità **push** dipendiamo dalla rappresentazione interna del Subject;
- nella modalità **pull** dipendiamo dalla classe concreta del Subject.

Poiché l'ultima dipendenza non è facilmente eliminabile, piuttosto che lasciarla nascosta nel casting conviene **esplicitarla**:
- all’interno dell’Observer salvo l’istanza di Observable a cui mi sono sottoscritto, così al momento dell’`update` posso verificare direttamente che l’istanza sia quella al posto di fare un casting;
- creiamo una classe `State` e l’aggreghiamo sia nell’Observer che nell’Observable concreto in modo che essa nasconda la rappresentazione reale dello stato.

Otteniamo dunque un codice simile al seguente:
```java
public class State { /* rappresentazione interna dello stato */ }

public class Observable {
    private State stato;
    private List<Observer> observers = new ArrayList<>();

    public void addObserver(@NotNull Observer obs) { observers.add(obs); }
    public void removeObserver(@NotNull Observer obs) { observers.remove(obs); }
    public void notifyObservers() {
        for (Observer obs: observers) update(this, stato);
    }
}

public class Subject extends Observable {
    public void setState(State nuovoStato) { ... }
    public State getState() { return super.stato; }
    /* Opzionale: altri metodi getter */
}

public interface Observer {
    public void update(Observable subject, Object stato);
}

public class ConcreteObserver {
    private Observable mySubject;

    @Override
    public void update(Observable subject, Object stato) {
        if (subject == mySubject) {
            ...
        }
    }
}
```

### Versione generica del pattern Observer

È possibile sfruttare i **generici** per evitare l’utilizzo dell’`instanceof`, evitando cosi l’utilizzo del casting (l’`instanceof` è un casting implicito di fatto), che di norma è una brutta pratica. Utilizzando i generici è possibile fare in modo che il tipo venga dichiarato al momento della creazione, in modo che i **controlli statici** verranno fatti su quel tipo, e quindi **non verranno più eseguiti a runtime** tramite l’`instanceof`; in questo modo il problema della dipendenza visto fino ad ora non si presenta più.

Ecco quindi la **parte fredda** del pattern Observer sfruttando i generici:
[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/1aa6ac0bcd7a8895f0e4754c733ac6120927adbc.svg)]

Utilizzando due interfacce è possibile rendere questo pattern il più possibile generico e implementabile in ogni situazione.
```Java
interface Observable<T> {
    void addObserver(Observer<T> observer);
    void removeObserver(Observer<T> observer);
    void notifyObservers();
    T getState();
}

interface Observer<T> {
    void update(Observable<T> model, T state);
}
```

### Come usarlo?

Esempio con uno stato che rappresenta una temperatura:
```Java
public class State {
    private double temp;
    
    public State(double temp) { this.temp = temp; }
    
    public double getTemp() { return temp; }
    
    public void setTemp(double temp) { this.temp = temp; }
}
```

Lo stato viene poi reso osservabile tramite l’interfaccia appena mostrata. 
Viene sfruttato anche il pattern [[Adapter]] perché vengono mappati alcuni metodi dello stato sui metodi dell’interfaccia Observable:
```Java
public class Model extends State implements Observable<Double> {
    private final List<Observer<Double>> observers = new ArrayList<>();
    
    @Override public void addObserver(Observer<Double> observer) {
        observers.add(observer);
    }
    
    @Override public void removeObserver(Observer<Double> observer) {
        observers.remove(observer);
    }

    @Override public void notifyObservers() {
        for (Observer<State> observer : observers)
            observer.update(this, getState());
    }

    @Override public Double getState() {
        return getTemp();
    }
    
    @Override public void setTemp(Double state) {
        super.setTemp(state);
        notifyObservers();
    }
}
```

L’unico difetto di questa implementazione è che all’esecuzione di `notifyObservers` nel metodo `setTemp` non vi è la certezza che il valore sia cambiato (es. stessa temperatura).