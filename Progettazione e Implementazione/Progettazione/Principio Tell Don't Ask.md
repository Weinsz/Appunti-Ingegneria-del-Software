> Non chiedere i dati, ma dì cosa vuoi che si faccia sui dati.
https://martinfowler.com/bliki/TellDontAsk.html


![Tell-Don’t-Ask](https://marcobuster.github.io/sweng/assets/07_tell-dont-ask.png)


Il responsabile di un'informazione è anche responsabile di tutte le operazioni su di essa.
Il principio Tell Don't Ask sancisce che, piuttosto di **chiedere** (*don't ask*) a un oggetto dei dati e fare operazioni con quei dati, è meglio dire (*tell*) a quest'oggetto cosa fare coi dati che contiene.

### Esempio con Deck e Card

Se voglio stampare il contenuto di tutte le carte in un mazzo:
```java
class Main {
    public static void main(String[] args) {
        Deck deck = new Deck();
        Card card = new Card();

        card.setSuit(Suit.DIAMONDS);
        card.setRank(Rank.THREE);
        deck.getCards().add(card);
        deck.getCards().add(new Card()); // <-- !!!

        System.out.println("There are " + deck.getCards().size() + " cards:");
        for (Card currentCard : deck.getCards()) {
            System.out.println(
                currentCard.getRank() + 
                " of " + 
                currentCard.getSuit()
            );
        }
    }
}
```

All’interno del ciclo ottengo gli attributi della carta e li uso per stampare le sue informazioni. Inoltre, nella riga evidenziata viene aggiunta una carta senza settare i suoi attributi. 
La responsabilità della gestione dell’informazione della carta è quindi **erroneamente delegata** alla classe chiamante `Main`.

Per risolvere, è possibile trasformare la classe `Card` nel seguente modo:
```java
class Card {
    private Suit suit;
    private Rank rank;

    public Card(@NotNull Suit s, @NotNull Rank r) {
        suit = s;
        rank = r;
    }

    @Override
    public String toString() {
        return rank + " of " + suit;
    }
}
```

L’informazione viene ora interamente gestita dalla classe `Card`, che la gestisce nel metodo `toString()` per ritornare la sua rappresentazione testuale.