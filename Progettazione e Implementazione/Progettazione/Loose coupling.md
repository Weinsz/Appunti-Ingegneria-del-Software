Il **loose coupling** è la capacità di una variabile o di un parametro di accettare l'assegnamento di oggetti aventi tipo diverso da quello della variabile/parametro, a patto che l'oggetto sia un sottotipo.

```java
Deck deck = new Deck();
CardSource source = deck;
List<Card> cards = drawCards(deck, 5);
```