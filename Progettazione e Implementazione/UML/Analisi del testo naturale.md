#### Come organizzare la partenza del design suddividendo in classi e responsabilità?

Due approcci principali:
1. [[Design Pattern]]: riconoscere una situazione comune da una data
2. [[Test Driven Development (TDD)]]: partendo dalla soluzione più immediata e semplice si definiscono classi solo all'occorrenza

Un’altra tecnica è l’**estrazione dei nomi** (***noun extraction***), per un certo senso _naïve_ ma adatta in caso di storie complesse.

### Noun extraction

Basandosi sulle **specifiche**, come i commenti esplicativi delle user stories:
- si parte dai sostantivi o frasi sostantivizzate;
- si sfoltiscono con certi criteri di sfoltimento;
- si cercano le relazioni tra loro (probabilmente date dai verbi) e quindi si produce la gerarchia delle classi.

Per spiegare il procedimento si consideri il seguente esempio, in cui vengono evidenziati i sostantivi e le frasi sostantivizzate:
> - _The **library** contains **books** and **journals**. > It may have several **copies** of a given book. > Some of the books are for **short term loans** only. > All other books may be borrowed by any **library member** for three **weeks**._
> - _**Members of the library** can normally borrow up to six **items** at a time, but **members of staff** may borrow up to 12 items at one time. > Only member of staff may borrow journals._
> - _The **system** must keep track of when books and journals are borrowed and returned, enforcing the **rules** described above._
>   
> tratto da Stevens, Pooley - Using UML


#### Criteri di sfoltimento

I criteri di sfoltimento servono per diminuire il numero di sostantivi considerando solo quelli rilevanti e più adatti per risolvere il problema. In questa fase, in caso di dubbi si può posticipare la decisione. Di seguito se ne riportano alcuni:
- **Ridondanza**: sinonimi, termini diversi per indicare lo stesso concetto. Anche se è stata utilizzata una parola diversa potrebbe essere comunque ridondante, soprattutto in lingue diverse dall’inglese in cui ci sono molti sinonimi. Nell’esempio: _library member_ e _member of the library_, _loan_ e _short term loan_.
- **Vaghezza**: nomi generici, comuni a qualunque specifica; potrebbero essere sintomo di una _classe comune astratta_. Nell’esempio: items.
- **Nomi di eventi e operazioni**: nomi che indicano *azioni* e non hanno un concetto di _stato_. Nell’esempio: _loan_.
- **Metalinguaggio**: parti _statiche_ che fanno parte della logica del programma e che quindi non necessitano di essere rappresentati come classi. Nell’esempio: _system_, _rules_.
- **Esterne al sistema**: concetti esterni o verità _“assolute”_ al di fuori del controllo del programma. Nell’esempio: _library_, _week_ (sempre di 7 giorni).
- **Attributi**: informazioni atomiche e primitive (stringhe, interi…) relative a una classe, che quindi non necessitano la creazione di una classe di per sé. Nell’esempio: _name of the member_ (se ci fosse stato).

Al termine di questa fase, si avrà dunque una lista di classi _"certe"_ e _"incerte"_. 
In questo esempio, sono sopravvissuti i termini _journal_, _book_, _copy_ (of _book_), _library member_ e _member of staff_.


#### Relazioni tra classi

Il prossimo passo è definire le relazioni tra le classi: inizialmente si collegano con delle _linee_ (non frecce) senza specificare la direzione dell’associazione. Parliamo di **associazioni** e non **attributi** perché non è necessariamente vero che tutte le associazioni si trasformino in attributi.

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/fcfb85f6886da995828ad862596f1a91eb0299d5.svg)]

Il prossimo passo è specificare le **cardinalità** delle relazioni, come specificato dal linguaggio UML (opposto in questo aspetto al diagramma ER). 
La precisione richiesta in questo punto è soggettiva: da una parte, specificare puntualmente il numero massimo di elementi di una associazione può aiutare a ottimizzare successivamente, dall’altra porta confusione.

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/fb9ab18a18e6663d6af88de08796b27c5d59b105.svg)]

Dopo aver ragionato sulle cardinalità, si iniziano a cercare **generalizzazioni** e **fattorizzazioni**. In questo caso, si nota che:
- `StaffMember` **IS_A** `LibraryMember` con in più la possibilità di prendere `Journal`. Inoltre, un altro indicatore è che hanno lo stesso tipo di relazioni con gli altri oggetti.
- `BorrowableItem` è un termine generico per indicare `CopyOfBook` e `Journal`.

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/69929dcec439a4a448c516a7c9fbd014c4e22c4c.svg)]

Distinguere `CopyOfBook` e `Journal` è inutile, perché di fatto un `Journal` _è una copia di_ un giornale. Si può quindi fattorizzare **rimuovendo la generalizzazione**, come mostrato di seguito:

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/65c5ffe2b723ce22961ef1c696f760d21e93e1b7.svg)]

È importante però preoccuparsi delle **cardinalità** delle relazioni: è sì vero che un `BorrowableItem` può non _essere una copia di_ un `Book` e di un `Journal`, ma **deve essere copia di _esattamente_ una delle due opzioni**. 
UML prevede un **linguaggio OCL** ([Object Constraint Language](https://en.wikipedia.org/wiki/Object_Constraint_Language)) per esprimere vincoli altrimenti impossibili da esprimere in un diagramma. Si può anche scrivere il _constraint_ in linguaggio naturale come **nota**.


### Stato: concreto vs astratto

Considerando una singola classe (anche articolata), ciò che ne caratterizza la **complessità** è il numero di situazioni in cui si può trovare, o per meglio dire, **il numero di stati che può assumere**. È possibile fare una distinzione tra:
- **stato concreto**: il prodotto scalare di tutti i possibili valori degli attributi della classe definisce i diversi stati, la caratteristica di questa tipologia di stati è che il numero di combinazioni esplode molto velocemente. Questo lo si può capire da un semplice esempio, nel caso in cui si avesse a disposizione un solo intero il numero di stati possibili sarebbe $2^{32}$, ma dal momento che gli attributi diventano due, il numero di stati risulterebbe essere $2^{32}∗2^{32}=2^{64}$. Visto l’esagerato numero di stati concreti è chiaro che non è necessario considerare ognuno di essi per capire cosa sta succedendo nel sistema.
- **stato astratto**: rappresenta i possibili stati del sistema tramite una visione più generale, sfruttando un sottoinsieme arbitrario _significativo_ degli stati concreti. Un esempio potrebbe essere quello della libreria visto in precedenza, andando a considerare tutti i libri la cui segnatura inizi per ‘L’, e si considerano questi come i libri disponibili per la sola lettura in sala; in questo modo non è necessario verificare ognuno di essi, ma per determinare lo stato è necessario verificare questa semplice condizione.

### Casi particolari

Esistono casi particolari riguardo il concetto di stato:
- **Stateless object**: oggetti che non possiedono attributi, di conseguenza sono privi di uno stato. Questi oggetti sono detti anche oggetti funzione e rappresentano delle **astrazioni funzionali** di qualcosa.
- **Oggetti immutabili**: oggetti che hanno un unico stato che non può cambiare. È importante distinguere una _Classe immutabile_ da un _Oggetto immutabile_: infatti prendendo come esempio la classe `String` è possibile dire che **la _classe_ ha infiniti stati** perché è possibile generare un numero quasi infinito di stringhe (tutte le permutazioni di serie di (fino a $2^{32}$) caratteri), mentre **un _oggetto_ di tipo `String` non può essere in alcun modo modificato** dopo essere stato istanziato.