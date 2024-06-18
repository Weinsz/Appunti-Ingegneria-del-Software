- **Tipologia:** Strutturale
- **Scopo:** Consente di inserire più oggetti in memoria condividendo parti di stato comuni tra più oggetti invece di conservare tutti i dati in ogni oggetto.

> Flyweight è un design pattern consistente in un oggetto che riduce al minimo l'uso della memoria condividendo quanti più dati possibile con altri oggetti simili; è un modo per utilizzare oggetti in gran numero quando una semplice rappresentazione ripetuta utilizzerebbe una quantità di memoria inaccettabile.
> -Wikipedia

A volte ci si trova in una situazione simile a quella che aveva ispirato il pattern [[Singleton]]: si ha una **serie di oggetti immutabili fortemente condivisi** all’interno del programma e per motivi di **performance** e **risparmio di memoria** vorremmo che **non esistano istanze diverse con lo stesso stato**. Se due client devono usare un’istanza con lo stesso stato, cioè vorremmo non usino ciascuno un’istanza duplicata ma proprio la **stessa istanza**, essendo le **istanze immutabili** tale condivisione non dovrebbe infatti creare alcun tipo di problema.

### Pattern

Il pattern **Flyweight** serve a **gestire una collezione di oggetti immutabili assicurandone l’unicità**: esso consiste nel rendere privato il costruttore e **costruire tutte le istanze a priori con un costruttore statico**, salvandole in una lista privata. 
I client possono dunque richiedere una certa istanza con un metodo `get` specificando lo stato dell’istanza desiderata: in questo modo, a parità di richiesta verranno restituite le stesse identiche istanze.

### Esempio con Card

Si è vista un’applicazione di questo pattern durante i laboratori parlando di `Card`:
```java
public class Card {
    private static final Card[][] CARDS = new Card[Suit.values().length][Rank.values().length];
    private final Rank rank;
    private final Suit suit;

	// Costruisco la matrice di possibili carte
    // per ogni seme ho un array di valori
    static {
        for (Suit suit : Suit.values()) {
            for (Rank rank : Rank.values()) {
                CARDS[suit.ordinal()][rank.ordinal()] = new Card(rank, suit);
            }
        }
    }

    // Costruttore privato
    private Card(Rank rank, Suit suit) {
        this.rank = rank;
        this.suit = suit;
    }

    // Metodo statico get che prende l'istanza con un certo stato
    public static Card get(Rank rank, Suit suit){
        assert rank != null && suit != null;
        return CARDS[suit.ordinal()][rank.ordinal()];
    }

    public Rank getRank() {
        return rank;
    }

    public Suit getSuit() {
        return suit;
    }

    @Override
    public String toString() {
        return rank +", "+suit;
    }
}

...

Card assoDiFiori = Card.get(Rank.ACE, Suit.CLUBS);
Card setteDiCuori = Card.get(Rank.SEVEN, Suit.HEARTS);
```

A differenza del pattern [[Singleton]] è difficile definire a priori quante istanze ci sono: abbiamo un’istanza per ogni possibile combinazione dei valori degli attributi che compongono lo stato. Proprio per questo motivo il pattern può risultare un po’ inefficiente per oggetti con rappresentazioni grandi: alla prima computazione vengono infatti inizializzati **tutti** gli oggetti, perdendo un po’ di tempo e sprecando potenzialmente spazio se non saranno accedute tutte le istanze.
