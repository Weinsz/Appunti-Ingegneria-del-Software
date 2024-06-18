- **Tipologia:** Comportamentale
- **Scopo:** I riferimenti `null` devono essere controllati per assicurarsi che non siano nulli prima di richiamare qualsiasi metodo, poiché i metodi non possono essere richiamati su riferimenti null, altrimenti viene lanciata una `NullPointerException`.

> Nella programmazione orientata agli oggetti, un oggetto nullo è un oggetto senza valore referenziato o con un comportamento definito neutro ('null'). Il Null Object pattern descrive gli usi di tali oggetti e il loro comportamento (o la loro assenza).
> - Wikipedia


### Nullability

Spesso si ha bisogno di utilizzare valori *nulli*. Ad esempio al termine di una [[Chain of responsibility]], dove per terminare la catena bisogna dare un valore nullo al `next` del prossimo gestore.
In generale, a una variabile che indica un riferimento a un oggetto, si può assegnare il valore `null` (valore di default di ogni oggetto quando non ancora assegnato) per indicare che essa non punta a niente.

Si ha un problema però quando a runtime si prova a dereferenziare tale valore e viene sollevata l'eccezione `NullPointerException`. Quest'evenienza ci costringe nel codice ad essere sempre molto titubanti sui valori che vengono passati, in quanto non si sa se essi puntino a un valore reale, dunque bisogna sempre controllare che non siano nulli. Bisogna dunque scegliere se adottare [[Contract based design vs programmazione difensiva|programmazione difensiva o a contratti]].

C’è però da dire che anche con tali accortezze l’utilizzo di `null` non è ideale, in quanto un valore nullo può indicare cose anche molto diverse:
- errore a runtime;
- stato temporaneamente inconsistente;
- valore assente o non valido.

Dunque  un codice chiaro non dovrebbe fare uso di `null`, o per lo meno dovrebbe limitarlo il più possibile. Le strategie di gestione dei nulli variano molto a seconda del significato assegnato a esso.

Quando **non ci sono valori assenti** e quindi il `null` indica solo **un errore** è sufficiente controllare che i dati passati non siano nulli attraverso:
- **condizioni**: se ben scritte sono una buona soluzione ma non la migliore.
- **asserzioni**: stesso effetto delle condizioni *if*, ma permettono di essere considerate nella compilazione in base alla circostanza; risulta utile usarle nel [[Prodotto e Processo/eXtreme Programming/Tecniche/Testing|Testing]] ma non nella release, in quanto ormai a quel punto si è certi di non finire mai in questo caso.
- **annotazione**: `@NotNull` è un annotazione che viene messa a disposizione da IntelliJ (ma non solo questo IDE la mette a disposizione), anche questa è un’ottima soluzione poiché l’IDE indicherà se sono presenti dei punti in cui un oggetto assume valore nullo, questo ancora **prima della compilazione**, e di conseguenza sarà possibile individuare il problema durante la fase di scrittura del codice.![null object valori non assenti](https://marcobuster.github.io/sweng/assets/09_nullObject-valori-non-assenti.png)

Quando **ci sono valori assenti**, ovvero che indicano situazioni particolari (es. il *joker* in un mazzo di carte, che non ha né rank né suit), la gestione è più complessa. Se non si vuole trattarli come `null` per via della sua ambiguità, una prima soluzione potrebbe essere quella di creare un metodo booleano nella classe che verifica se l'istanza ha il valore nullo (es. `isJoker()`). Quest'approccio apre le porte ad errori da parte dell'utente, che potrebbe non effettuare il controllo prima di usare l'oggetto. 

> [!NOTE] Optional
> Una soluzione migliore sfrutta gli [**Optional type**](https://docs.oracle.com/en/java/javase/21/docs//api/java.base/java/util/Optional.html) (da Java 8), che consiste in un oggetto che potrebbe **o meno** contenere un valore non nullo. Viene usato principalmente come valore di ritorno per metodi che potrebbero restituire “nessun valore” (se usati come parametri potrebbero esservi [diverse casistiche da considerare](https://rules.sonarsource.com/java/RSPEC-3553/), quindi meglio non farlo), inoltre questi oggetti optional non dovrebbero mai essere nulli, ma dovrebbero sempre puntare a un'istanza di un oggetto optional.
> 
> Al posto del **costruttore** definisce 3 metodi statici:
> - `static <T> Optional<T> empty()` che restituisce un’istanza vuota di un oggetto optional;
> - `static <T> Optional<T> of(T value)` restituisce un oggetto optional che descrive un valore non nullo del tipo passato come parametro;
> - `static <T> Optional<T> ofNullable(T value)` restituisce un oggetto optional che descrive un valore del tipo passato come parametro, ma solo se questo non è nullo, altrimenti restituisce un oggetto optional.
> 
> Inoltre la classe optional fornisce diversi metodi, i più degni di nota sono i seguenti:
> - `T get()` restituisce il valore se presente, altrimenti solleva l’eccezione `NoSuchElementException`;
> - `boolean isEmpty()` restituisce true se il valore non è presente, false altrimenti;
> - `boolean isPresent()` restituisce true se il valore è presente, false altrimenti;
> - `T orElse(T other)` restituisce il valore se presente, altrimenti restituisce il valore di tipo T passato.

## Pattern Null Object

La soluzione più elegante, ma non sempre applicabile facilmente, per creare un oggetto che corrisponda al **concetto di nessun valore** o **valore neutro** sfrutta il pattern **Null Object**. Esso consiste nella creazione all’interno della classe o dell’interfaccia di un _oggetto statico_ (solitamente chiamato `NULL` o `DEFAULT`) che rappresenta il concetto di _valore nullo_, e quindi va di fatto a sostituire `null`. 
Questo oggetto fornisce _particolari implementazioni dei metodi_ dell’interfaccia per realizzare l’idea di *valore nullo* a livello di dominio. Così tale oggetto mantiene l’identità della classe rimanendo però sufficientemente separato dagli altri valori; inoltre, la presenza di implementazioni specifiche dei metodi evita il lancio di eccezioni ambigue.

```java
public interface CardSource {
    Card draw();
    boolean isEmpty();

    public static CardSource NULL = new CardSource() {
        public boolean isEmpty() { 
            return true; 
        }
        public Card draw() {
            assert !isEmpty();
            return null;
        }
    };
}
```

Quindi il concetto del Null Object pattern è quello di creare un oggetto valido di un tipo anonimo (`CardSource.NULL`, che aderisce alla interfaccia `CardSource`) in cui viene definito un comportamento specifico per ogni metodo, che rispecchia ciò che accadrebbe nel caso in cui il metodo venisse chiamato su `null` nel normale flusso di istruzioni.

Una particolarità dell’esempio riportato qui sopra è che il pattern è realizzato tramite un _attributo dell’interfaccia_, che deve essere obbligatoriamente statico e pubblico (in realtà non serve specificarlo, lo è già).


### Esempio di uso

- Senza pattern:
```java

Card x = deck.draw();
if (x != null)
	System.out.print(x.desc());
else System.out.print("Carta non esistente");


Card draw() {
	if (isEmpty())
		return null;
	else return internal.remove(0);
}
```

- Con Null Object:
```java
Card x = deck.draw();
System.out.print(x.desc());


Card draw() {
	if (isEmpty())
		return Card.NULL;
	else return internal.remove(0);
}

static Card NULL = new Card() {
	public String desc() { return "Carta non esistente"; }
};
```