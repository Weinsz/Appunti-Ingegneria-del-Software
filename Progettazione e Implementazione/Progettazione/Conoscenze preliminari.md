### Object orientation

^6e76cf

Un linguaggio per essere definito **object oriented** deve soddisfare 3 proprietà:
1. **Ereditarietà**: cioè la possibilità di poter definire una classe ereditando proprietà e comportamenti di un'altra classe.
2. **Polimorfismo**: quando una classe può assumere diverse forme in base alle interfacce che implementa. Esempio *tennista scacchista*: in un torneo di tennis è poco utile sostituire una persona che gioca a tennis e a scacchi (dunque una classe che implementa entrambe le interfacce) con una che gioca sia a tennis che a scacchi (basta sappia fare la prima).
   Il collegamento tra capacità e oggetto è fatto **a tempo di compilazione**, dunque non è importante se la capacità non è ancora stata definita.
3. **Collegamento dinamico**: anche detto *late binding* o polimorfismo a runtime; in Java il tipo concreto degli oggetti può non essere specificato staticamente e quindi il problema di stabilire **quale metodo chiamare** viene risolto **a tempo d'esecuzione** (*runtime*) dalla JVM. Es. in C++ si esplicita con *virtual*. 
   Promuove la flessibilità del codice, poiché si possono aggiungere nuove sottoclassi senza modificare il codice esistente che funziona con la superclasse. Facilita inoltre l'estensibilità, poiché è possibile aggiungere nuovi comportamenti sovrascrivendo i metodi all'interno delle sottoclassi.


### Principi Solid

^0a9782

^d4ff78
1. **Single Responsibility**: una classe ha **un solo scopo/responsabilità**. Così facendo, le classi rimangono semplici e si agevola la riusabilità. In altri termini, deve avere un solo motivo per essere cambiata. ^62f6b3
2. **Open-Closed Principle**: le classi devono essere aperte ai cambiamenti (*open*) ma senza modificare le parti già consegnate e in produzione (closed). Si può quindi fare [[Progettazione e Implementazione/Progettazione/Refactoring|Refactoring]] ma deve essere preferibile **estendere la classe attuale**. ^14625c
3. **Liskov Substitution Principle**: c'è la garanzia che le caratteristiche ereditate dalla classe padre continuino ad esistere nelle classi figlie. Si collega all'aspetto **contract-based** delle [[Metodologie Agile]]: le **pre-condizioni** di un metodo di una classe figlia devono essere ugualmente o meno restrittive del metodo della classe padre. Al contrario, le **post-condizioni** di un metodo della classe figlia non possono garantire più di quello che garantiva il metodo nella classe padre. Fare _casting_ bypassa queste regole. ^16f5b7
4. **Interface Segregation**: invece che avere un'unica interfaccia con tanti metodi, si creano più interfacce ridotte. Meglio quindi avere **tante interfacce specifiche** e piccole (composte da pochi metodi), piuttosto che poche, grandi e generali. Questo evita di dover implementare metodi che non vengono realmente utilizzati e di lanciare l'eccezione `NotImplementedException`, e sarà più semplice utilizzare le interfacce in contesti differenti.
5. **Dependency Inversion**: il codice dal quale una classe dipende non deve essere più concreto di questa classe. Dunque classi concrete devono tendenzialmente dipendere da astrazioni (es. interfacce) e non da altre classi concrete.
   Per esempio, se il _telaio della FIAT 500_ dipende da uno specifico motore, è possibile utilizzarlo solo per quel specifico motore. Se invece il telaio dipende da _un_ concetto di motore, non c’è questa limitazione.
   
>    Il principio fu formulato per la prima volta da Robert C. Martin, che lo sintetizzò nel seguente modo:
>    - I moduli di alto livello non devono dipendere da quelli di basso livello. Entrambi devono dipendere da astrazioni;
>    - Le astrazioni non devono dipendere dai dettagli; sono i dettagli che dipendono dalle astrazioni. ^5f2600

### Reference escaping

Il _reference escaping_ è una violazione dell’incapsulamento.

Basandoci sull’esempio del mazzo di carte, si vuole che la sua implementazione resti **segreta**, quindi ecco i possibili _errori_ affinché non venga rispettata questa condizione:
- quando un getter ritorna un riferimento a un segreto;
```java
public Deck {
    private List<Card> cards;
        
    public List<Card> getCards() {
        return this.cards;
    }
}
```

- quando un setter assegna a un segreto un riferimento che gli viene passato;
```java
public Deck {
    private List<Card> cards;

    public setCards(List<Card> cards) {
        this.cards = cards;
    }
}
```

- quando il costruttore assegna al segreto un riferimento che gli viene passato;
```java
public Deck {
    private List<Card> cards;

    public Deck(List<Card> cards) {
        this.cards = cards;
    }
}
```

### Encapsulation e information hiding

**Legge di Parnas (L8)**
> _Solo ciò che è nascosto può essere cambiato liberamente e senza pericoli._

Lo stato mostrato all’esterno non può essere modificato, mentre quello nascosto sì.
Questo principio serve per **facilitare la comprensione del codice** e renderne più facile la modifica parziale senza fare danni. Dovrà essere quindi chiarito prima dell’implementazione ciò che sarà **pubblico** e ciò che invece sarà **privato**.

### Legacy o deprecated

Una classe o una funzionalità, dopo diverse modifiche nel tempo, può arrivare a un punto di non ritorno, dove l’evoluzione si ferma per diversi motivi, come un design iniziale troppo limitante o l’arrivo di un'innovazione tecnologica.

In questi casi la classe o funzione può essere chiamata:
- **Legacy**: una classe di questo genere continuerà a funzionare e **sarà supportata**, però verrà consigliato l’utilizzo di un altra classe più recente.
- **Deprecated**: in questo caso la classe resterà comunque funzionante ma **non sarà più supportata**. Il suo utilizzo sarà fortemente **sconsigliato** e si spingerà il dev a fare un [[Progettazione e Implementazione/Progettazione/Refactoring|Refactoring]] del codice laddove è presente la funzione deprecata. Essa deve essere sostituita con la nuova classe standard, perché dopo un certo lasso di tempo verrà rimossa o la sua funzionalità non sarà più garantita.


### Immutabilità

Una classe è **immutabile** quando non si può modificare lo stato di ogni suo oggetto dopo la creazione. Questo ci garantisce grandi vantaggi, come ad esempio condividere oggetti senza il rischio che il suo stato venga modificato (in caso venisse modificato, l’encapsulation potrebbe non essere rispettata), quindi sarà fondamentale _massimizzare_ l’utilizzo di questo tipo di classi.

Per assicurare tale proprietà è necessario:
- **non fornire metodi di modifica** allo stato;
- avere tutti gli **attributi privati** per i tipi potenzialmente mutabili (come liste) e fornire solo il valore tramite i _getter_ e non il riferimento;
- avere tutti gli **attributi final** se non già privati;
- assicurare l’**accesso esclusivo** a tutte le parti non immutabili, cioè non avere **reference escaping**.


### Code smell

I _code smell_ sono dei segnali che suggeriscono **problemi nella progettazione del codice**, mantenere questi problemi nel codice significa aumentare il **debito tecnico**. Di seguito ne sono elencati alcuni:
- **codice duplicato**: si può fare per arrivare velocemente al verde quando si usa il [[Test Driven Development (TDD)|TDD]], ma è da rimuovere con il [[Progettazione e Implementazione/Progettazione/Refactoring|Refactoring]]. Rischia di portarsi dietro degli errori o particolarità legate al primo uso di questo codice. È dunque importante cercare di fattorizzare il più possibile.
- **metodi troppo lunghi**: non è un vincolo stretto dato che dipende dai casi, ma solitamente sono poco leggibili e poco riusabili;
- **troppi livelli di indentazione**: scarsa leggibilità e riusabilità, è bene fattorizzare il codice invece che avere una serie di if e for _innestati_ che lo rendono confusionario, quindi è meglio creare dei metodi con nomi chiari per evitare ciò.
- **troppi attributi**: suggerisce che la classe non rispetta la single responsibility, cioè fa troppe cose;
- **lunghe sequenze di _if-else_ o _switch_**: possono essere sostituiti da strutture basate su **polimorfismo** e **collegamento dinamico**;
- **classe troppo grande**;
- **lista parametri troppo lunga**: se proprio ne ho bisogno meglio raggrupparli in una struttura e passarli come unico parametro;
- **numeri "magici"**: è importante assegnare alle costanti numeriche all’interno del codice un nome per comprendere meglio il loro scopo, infatti dei semplici numeri possono avere significati diversi in base al loro contesto, ad esempio uno zero può indicare il suo valore numerico, l’assenza di valori o `null`;
- **commenti che spiegano cosa fa il codice**: indica/ammette che il codice non è abbastanza chiaro;
- **nomi oscuri o inconsistenti**;
- **codice morto**: nel programma non deve essere presente del codice irraggiungibile, commentato o non testato. Questo appesantisce il progetto o porta a possibili rischi ed è quindi preferibile eliminarlo. Nel caso in cui dovesse tornare utile è possibile recuperarlo utilizzando strumenti di versioning, accedendo a commit precedenti alla sua cancellazione.
- **getter e setter**: Questi metodi causano la perdita dell’encapsulation e information hiding, perché esportano esternamente il segreto contenuto nella classe. Sono utili nella fase preliminare della stesura del codice, è importante rimuoverli per far spazio a dei **metodi che permettano all’utente di eseguire una specifica operazione** da lui richiesta, piuttosto che fornirgli il dato e permettergli di elaborarlo come meglio crede ([[Principio Tell Don't Ask]]).

Link utili per approfondire i code smell:
- [Refactoring Guru](https://refactoring.guru/refactoring/smells)
- [Wikipedia](https://en.wikipedia.org/wiki/Code_smell)
- [Luzkan](https://luzkan.github.io/smells/)