- **Tipologia:** Strutturale
- **Scopo:** Permette la collaborazione tra oggetti con interfacce incompatibili, detto anche Wrapper

> Nell'ingegneria del software, è un design pattern che consente di utilizzare l'interfaccia di una classe esistente come un'altra interfaccia. Viene spesso utilizzato per far funzionare le classi esistenti con altre senza modificare il loro codice sorgente.
> - Wikipedia

### Problema
Immagina di creare un'app per il monitoraggio del mercato azionario. L'app scarica i dati azionari da più fonti in formato _**XML**_ e quindi visualizza grafici e diagrammi per l'utente.
Ad un certo punto, decidi di migliorare l'app integrando una libreria di analisi intelligente di terze parti. Ma c'è un problema: la libreria di analisi funziona solo con dati in formato _**JSON**_.
È possibile modificare la libreria in modo che funzioni con XML. Tuttavia, ciò potrebbe rompere parte del codice esistente che si basa sulla libreria. E peggio, potresti non avere accesso al codice sorgente della libreria in primo luogo, rendendo questo approccio impossibile.

Spesso capita di dover **far collaborare interfacce diverse** di componenti non originariamente sviluppati per lavorare insieme. Questo capita in moltissime situazioni, ma volendone citare alcune:
- ambito di sviluppo [[Modello COTS|COTS (Component Off The Shelf)]]: si riutilizza tanti componenti disponibili sul mercato, non pensati per essere compatibili;
- sviluppando ed evolvendo un programma in modo _[[Modelli incrementali|incrementale]]_ capita di dover integrare nuovi componenti con altri vecchi (*legacy*) per garantire una certa continuità all'utente.

### Pattern

Da situazioni simili è nato il bisogno di creare delle strutture che permettessero di rendere compatibili componenti pre-esistenti, ovvero come andare a creare della **colla** in grado di legare i componenti tra loro per **soddisfare le specifiche** del sistema. Ben presto poi è scaturito il pattern **Adapter**, ormai diffuso, che consiste nel creare vari moduli che possano essere incollati o adattati ad altre strutture in modo da renderle utilizzabili incrementalmente e in modo controllato.

Viene spesso usato anche inconsciamente, in più ci sono due "versioni":
- **Class Adapter**: adatta una classe
- **Object Adapter**: adatta un oggetto di una classe

Questi due pattern sono molto simili a livello di schema UML ma abbastanza differenti da rendere importante capire quale usare a seconda dei contesti, comprendendo vantaggi e svantaggi di entrambi.


## Class Adapter
[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/83ff9d74f5c581bf7b609b7fa0f5f0cb4bc787f5.svg)]

Come si nota dall'UML, per permettere a un client di comunicare tramite un'interfaccia `Target` con un componente concreto **vecchio** detto `Adaptee`, il **Class Adapter** usa una classe concreta che **implementa l'interfaccia Target** ed **estende** la vecchia classe `Adaptee`, ereditandone dunque i metodi e la vecchia interfaccia. All'interno di Class Adapter si potrà quindi semplicemente **rimappare le funzionalità** richieste dalla nuova interfaccia su quella vecchia, implementando qualcosa solo se strettamente necessario e sfruttando la logica già presente della classe vecchia che si estende.
```java
public class Adapter extends Adaptee implements Target {
    @Override
    public void request() {
        this.oldRequest();
    }
}
```

Così il client userà l'Adapter come se fosse l'oggetto completo, non accorgendosi che quando ne chiama un metodo in realtà il codice eseguito è quello appartenente alla vecchia classe pre-esistente: **in un'unica istanza** si sono dunque riunite l'interfaccia vecchia e quella nuova.

### Pro e Contro

- Estendendo l'`Adaptee`, la classe `Adapter` ha parziale accesso alla sua rappresentazione interna, vantaggio non da poco considerando quanto ciò faciliti l'eventuale modifica di funzionalità; inoltre Adapter ne eredita le definizioni dei metodi, e se non vanno cambiati tra la vecchia e la nuova interfaccia, si risparmierà parecchio tempo e codice.

- Un'istanza della classe `Adapter` può essere utilizzata attraverso **entrambe le interfacce**, in quanto implementa quella nuova ed eredita quella vecchia; questo aspetto può essere considerato **sia un vantaggio che uno svantaggio**: 
	- da un lato ciò è molto utile in sistemi che evolvono incrementalmente e in cui dunque alcune componenti potrebbero volersi ancora riferire alla vecchia interfaccia
	- d'altro canto questo aspetto impedisce di imporre che l'oggetto sia utilizzato solo tramite l'interfaccia nuova.

- Quest'approccio perde un po' di senso nel caso in cui si debba adattare un'**interfaccia** e non una classe, in quanto implementare entrambe le interfacce non permette di ereditare codice o funzionalità da quella vecchia. 
  
Altri due problemi:
- sfrutta l'ereditarietà multipla, che non è supportata da tutti i linguaggi a oggetti (es. Java)
- quando `Target` e `Adaptee` possiedono lo stesso nome ma hanno comportamenti diversi, con una gestione particolarmente scomoda.


## Object Adapter
[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/fd8140a52ac43edf7a916959fb4d4c24aad56b6d.svg)]

Come abbiamo già detto più volte, spesso conviene prediligere la **composizione** rispetto all’ereditarietà: al pattern del Class Adapter si contrappone dunque l’**Object Adapter**, che invece di estendere la classe `Adaptee` **contiene una sua istanza** e **delega** ad essa tramite la vecchia interfaccia le chiamate ai metodi dell’interfaccia nuova, eventualmente operando le necessarie modifiche.

```java
public class ObjectAdapter implements Target {
    private final Adaptee adaptee;

    public Adapter(Adaptee adaptee) {
        assert adaptee != null;
        this.adaptee = adaptee;
    }

    @Override
    public void request() {
        adaptee.oldRequest();
    }
}

```

Anche qui il client non si accorge di nulla e specialmente non sarebbe nemmeno in grado di dire con certezza se l’Adapter utilizzato sia un Class Adapter o un Object Adapter: a lui la scelta del paradigma è del tutto **trasparente**.

### Pro e Contro

Punti di debolezza:
- invece di avere un'unica istanza che racchiuda entrambe le interfacce, con questo pattern si hanno due istanze (Adapter e Adaptee al suo interno), cosa che può costituire un notevole spreco di memoria in certe situazioni.
- aver sostituito l'ereditarietà con la composizione ha lo sgradevole effetto di non permettere
  all'`Adapter` di vedere in alcun modo la rappresentazione protetta dell' `Adaptee`, dunque potrà manipolarlo unicamente mediante la sua interfaccia pubblica. Si è poi costretti a **reimplementare ogni metodo** anche se questo non è cambiato dall’interfaccia vecchia a quella nuova, in quanto è comunque **necessario operare la delega all’Adaptee**.

Tuttavia, l’**Object Adapter** si rivela particolarmente utile se ad essere adattata debba essere un’_interfaccia_: non soffrendo di problemi di ereditarietà, un Object Adapter ha la peculiarità di poter adattare chiunque implementi la vecchia interfaccia, ovvero **un’intera _gerarchia_ di classi potenzialmente non ancora esistenti**.

### Class vs Object Adapter

**Class Adapter** e **Object Adapter** hanno ciascuno i propri vantaggi e svantaggi che li rendono più adatti ad essere utilizzati in diverse situazioni.
Confronto tra i due approcci riassunto nella seguente tabella:

| Aspetto                               | Class Adapter                                                                                      | Object Adapter                                                                                                 |
| ------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Accesso all'Adaptee**               | <span style="color:green">L'Adapter può accedere ad attributi e metodi segreti dell'Adaptee</span> | <span style="color:red">L'Adapter può interagire con l'Adaptee solo tramite la sua interfaccia pubblica</span> |
| **Riuso del codice**                  | <span style="color:green">Non richiede di reimplementare i metodi che non cambiano</span>          | <span style="color:red">Qualunque metodo va reimplementato per fare la delega</span>                           |
| **Uso della memoria**                 | <span style="color:green">Un'unica istanza</span>                                                  | <span style="color:red">Due istanze obbligatorie</span>                                                        |
| **Adozione delle interfacce**         | <span style="color:#ff9900">L'istanza può essere usata con entrambe le interfacce</span>           | <span style="color:#ff9900">L'istanza può essere usata solo tramite la nuova interfaccia</span>                |
| **Problemi di ereditarietà multipla** | <span style="color:red">Possibili</span>                                                           | <span style="color:green">Nessun problema</span>                                                               |
| **Adattamento delle interfacce**      | <span style="color:red">Non indicato per questo scopo</span>                                       | <span style="color:green">Adattando un'interfaccia si può adattare un'intera gerarchia di classi</span>        |
Inoltre:
- [[Conoscenze preliminari#^62f6b3|Single Responsibility Principle]]: È possibile separare l'interfaccia o il codice di conversione dei dati dalla logica primaria del programma.
- [[Conoscenze preliminari#^14625c|Open/Closed Principle]]: È possibile introdurre nuovi tipi di adapter nel programma senza rompere il codice client esistente, purché funzionino con gli adapter tramite l'interfaccia client.
- Adapter modifica l'interfaccia di un oggetto esistente, mentre [[Decorator]] migliora un oggetto senza modificarne l'interfaccia. Inoltre, Decorator supporta la composizione ricorsiva, che non è possibile quando si utilizza Adapter.
- [[Façade]] definisce una nuova interfaccia per gli oggetti esistenti, mentre Adapter tenta di rendere utilizzabile l'interfaccia esistente. Adapter di solito esegue il wrapping di un solo oggetto, mentre Façade funziona con un intero sottosistema di oggetti.