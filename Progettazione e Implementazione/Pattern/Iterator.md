- **Tipologia:** Comportamentale
- **Scopo:** Permette di accedere agli elementi di una collezione (oggetto Collection) in modo sequenziale senza bisogno di conoscere la sua rappresentazione interna sottostante. I contenitori possono fornire un'interfaccia iteratore indipendente dalla rappresentazione per fornire l'accesso agli elementi.

> Nella programmazione orientata agli oggetti, il pattern Iterator è un design pattern in cui un iteratore viene utilizzato per attraversare un container/collezione e accedere agli elementi al suo interno.
> - Wikipedia

Talvolta gli oggetti che definiamo fanno da **aggregatori** di altri oggetti, contenendo cioè una collezione di questi su cui poi fare certe operazioni: in questi casi è molto probabile che si voglia poi poter iterare sui singoli elementi aggregati, ma senza esporre la rappresentazione interna usata per contenerli. 
Esistono però altri casi in cui non si ha un aggregatore di oggetti ma è necessario che avvenga un’iterazione, questo è il caso della classe _Scanner_ di Java (che implementa l’interfaccia Iterator).

Il pattern Iterator nasce proprio per risolvere questo tipo di problematiche: esso consiste nella creazione di una classe `ConcreteIterator` che abbia accesso alla rappresentazione interna dell'oggetto e esponga i suoi elementi in modo sequenziale tramite i metodi `next()` e `hasNext()`; dovendo accedere alla rappresentazione, molto spesso tale iteratore si realizza come una _classe interna anonima_.

Java supporta largamente il pattern Iterator ([[Meta-pattern]] di tipo **unification**), a tal punto che nella libreria standard esiste un’interfaccia generica per gli iteratori, `Iterator<E>`, al cui interno sono definiti, oltre ai metodi di cui sopra, il metodo `remove()`, normalmente non supportato in quanto permetterebbe di modificare la collezione contenuta dalla classe, e il metodo `forEachRemaining()`, che esegue una data azione su tutti gli elementi ancora non estratti dell’iteratore.

Per questioni di chiarezza e semplicità, sarebbe meglio non includere il metodo `remove()` nell’interfaccia dell’iteratore poiché non ogni iteratore necessita di tale metodo; questo approccio va a violare il primo principio SOLID, ovvero il **Single Responsibility**. Sarebbe il caso di avere due interfacce differenti, una che estende l’altra, oppure due interfacce distinte chiamate ad esempio `Removable<E>` che rende una classe in grado di rimuovere degli elementi, e l’altra `Iterator<E>`. Nel caso in cui una classe implementi entrambe le interfacce sarà possibile avere un oggetto iterabile ma che allo stesso tempo fornisca la possibilità di rimuovere un elemento, ma sfortunatamente non è così in Java (penso a livello di API standard).

```java
public interface Iterator<E> {
    boolean hasNext();
    E next();

    default void remove() {
        throw new UnsupportedOperationException("remove");
    }

    /* aggiunta funzionale opzionale */
    default void forEachRemaining(Consumer<? super E> action) {
        Objects.requireNonNull(action);
        while (hasNext())
            action.accept(next());
    }
}
```

Esiste inoltre un’interfaccia che la classe può implementare, chiamata `Iterable<E>`: essa richiede solamente la presenza di un metodo `iterator()` che restituisca l’**iteratore concreto**, e una volta implementata permette di utilizzare il proprio oggetto aggregatore all’interno di un costrutto `foreach`.[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/a1c81927fa00b168e7c6bbb82edf938c5a678d27.svg)]

Così, per esempio, possiamo passare dal seguente codice:
```java
Iterator<Card> cardIterator = deck.getCards();
while (cardIterator.hasNext()) {
    Card card = cardIterator.next();
    System.out.println(card.getSuit());
}
```
a quest’altro:
```java
for (Card card : deck) {
    System.out.println(card.getSuit());
}
```

Oltre ad essere più breve il codice è molto più chiaro, rendendo evidente che la singola `card` sia read-only.

Un’osservazione interessante da fare riguardo ad una classe che implementa `Iterable<E>` è che la classe non può essere iterabile su due cose differenti, in quanto i tipi **generici** sono considerati **a tempo di compilazione**, ma successivamente per il meccanismo di *erasure* scompaiono, quindi nel codice finale i due tipi generici si sovrappongono. Di conseguenza, non possono essere distinti, perciò **non è possibile rendere una classe iterabile rispetto a cose diverse**.


### Pro vs Contro

### Pro
- [[Conoscenze preliminari#^62f6b3|Single Responsibility Principle]]: puoi ripulire il codice client e le collection estraendo algoritmi di attraversamento ingombranti in classi separate.
- [[Conoscenze preliminari#^14625c|Open/Closed Principle]]: puoi implementare nuovi tipi di collection e iteratori e passarli al codice esistente senza interrompere nulla.
- Puoi scorrere la stessa collection in parallelo perché ogni oggetto iteratore contiene il proprio stato di iterazione. Per lo stesso motivo, puoi ritardare un'iterazione e continuarla quando necessario.

### Contro

L'uso di un iteratore può essere meno efficiente rispetto all’accesso diretto agli elementi di alcune collection specializzate.