- **Tipologia:** Comportamentale ([[Meta-pattern]] con collegamento di tipo connection)
- **Scopo:** Permette di definire una famiglia di algoritmi, mettendo ciascuno di essi in una classe separata e rendendo i relativi oggetti intercambiabili.

> In programmazione, il pattern Strategy (noto anche come pattern di Delegation) è un software design pattern che consente di selezionare un algoritmo in fase di esecuzione, il più adatto.
> - Wikipedia

#### Esempio nel mondo reale

- Immagina di dover raggiungere l'aeroporto. Puoi prendere un autobus, ordinare un taxi o andare in bicicletta. Queste sono le tue strategie di trasporto. Puoi scegliere una delle strategie in base a fattori come budget o limiti di tempo.
### Duck Saga

Talvolta nelle nostre classi vogliamo definire **comportamenti diversi per diverse istanze**: la soluzione classica dei linguaggi Object-Oriented è la creazione di una gerarchia di classi in cui le classi figlie sovrascrivano i metodi della classe genitore. Tuttavia, questo espone a delle problematiche: cosa fare se per esempio la classe genitore cambia aggiungendo un metodo che una delle classi figlie non dovrebbe poter implementare? (es. `Duck` che ha come figlia `RubberDuck`, che aggiunge il metodo `fly()` che ovviamente non potrà essere utilizzato dalla figlia).

Così però si violerebbe l'[[Conoscenze preliminari#^14625c|Open/Closed Principle]], e non siamo intenzionati a rimuovere il metodo incriminato, per cui dobbiamo cercare altre soluzioni. 
Una prima idea sarebbe quella di sopperire al fatto che la classe genitore non sappia chi sono i suoi figli con costrutti propri del linguaggio:
- una classe `Final` non permette di ereditare, ma questo non ci permetterebbe di differenziare il comportamento per le diverse possibili istanze;
- una classe `Sealed` (aggiunta di Java 17) che permette di scegliere esplicitamente chi possano essere i suoi figli, specificandone il nome: in questo modo si ha controllo su chi saranno i figli e nell’implementare i nuovi metodi saprò sempre da chi verranno utilizzati successivamente, ma si tratta comunque di una soluzione parziale, che limita l’espandibilità del mio progetto, infatti non permetterò ad altri utenti, che non conosco, di creare classi figlie della mia classe.

Non si può neanche pensare di fare semplicemente l’**override** nella classe figlia del metodo aggiunto facendo in modo che lanci un’eccezione: si avrebbe infatti un'inaccettabile violazione del [[Conoscenze preliminari#^16f5b7|principio di sostituzione di Liskov]], che afferma sostanzialmente che un’istanza di una sottoclasse deve poter essere usata senza problemi al posto dell’istanza di una classe genitore (prima sapevo volare, ora sto dicendo che in questo caso non riesco).

Si potrebbe invece creare un interfaccia e non dare l’implementazione di default dei metodi, così facendo delego alle classi figlie la possibile implementazione dei metodi rischiosi (`fly` per la `RubberDuck` lancerebbe errore ad esempio), ma al costo di limitare la fattorizzazione. L’introduzione di una o più classi astratte per evitarlo andrebbe a complicare molto la gerarchia. Dovrò implementare il metodo in ogni classe figlia non potendolo più fare nel padre, quindi avrò del codice ripetuto.

Una soluzione migliore si basa invece sul concetto di **delega**, che sostituisce all’ereditarietà la **composizione**. Consiste nell'individuare ciò che cambia nell’applicazione e separarlo da ciò che rimane "fisso": si creano delle **interfacce per i comportamenti da diversificare** e una **classe concreta che implementa ogni diverso comportamento** possibile. All’interno della classe originale si introducono dunque degli **attributi di comportamento**, impostati al momento della costruzione o con dei setter a seconda della dinamicità che si vuole dare: quando viene richiesto il comportamento a tale classe, essa si limiterà a chiamare il proprio “oggetto di comportamento”. 

Nell’esempio delle `Duck`, per esempio, la struttura è la seguente:[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/712674f42f2325f9c9ba220ad145815c3cca66b7.svg)]

**Così facendo si preserva l'[[Conoscenze preliminari#^14625c|Open/Closed Principle]] e il [[Conoscenze preliminari#^5f2600|Dependency Inversion Principle]].**

Come si vede, qui non c’è scritto da nessuna parte che una `Duck` deve volare, ma solo che deve definire la sua “politica di volo” incorporando un `FlyBehaviour`.

Ovviamente la modifica della classe padre resta sempre rischiosa e va fatta studiando le circostanze e gli effetti del cambiamento. In un team **XP** idealmente dovrebbe essere meno problematica una modifica in quanto l’intero team condivide la conoscenza del progetto 
([[Proprietà collettiva]]), quindi si conoscono anche gli effetti causati da tale modifica (anche se la conoscenza non è mai assoluta). Nel caso di un progetto **open-source** invece bisogna trovare un modo per rendere pubblico a tutti coloro che hanno ereditato dalla classe modificata la possibilità che si possano verificare dei problemi.

### Delegation / Strategy

La differenziazione dei comportamenti si fa dunque **a livello d’istanza e non di classe**:

> Il pattern Strategy definisce una famiglia di algoritmi e li rende tra di loro intercambiabili tramite _encapsulation_. 

Per questo motivo tale pattern è usato in situazioni anche molto diverse da quella mostrata nell’esempio. Un’altra situazione in cui viene sfruttato questo pattern è l’interfaccia `Comparator` 
([compare()](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html#compare-T-T-) chiamato da `Collections.sort()`).

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/b8c7f4fed21d9f86f6579c144bf158d154cde46e.svg)]

È possibile notare nel diagramma UML che il client inizialmente conosce il concetto di `AbstractStrategy`, e in qualche modo (tramite costruttore, setter o altre metodologie) gli viene fornita un’implementazione di tale strategia. 

Questo pattern è applicabile in quelle situazioni in cui il client non deve conoscere in che modo una certa operazione viene fatta, ma basta soltanto che venga svolta. 
Nell’esempio del `Comparator` si può dire che basta che si possano comparare due oggetti, non importa il criterio di confronto, quello lo definisco io (senza usare l'ordinamento *naturale*, se già presente).


### Pro vs Contro

### Pro
- È possibile scambiare gli algoritmi utilizzati all'interno di un oggetto in fase di runtime.
- È possibile isolare i dettagli di implementazione di un algoritmo dal codice che lo utilizza.
- Puoi sostituire l'ereditarietà con la **composizione**.
- [[Conoscenze preliminari#^14625c|Open/Closed Principle]]: Puoi introdurre nuove strategie senza dover modificare la classe che avrà un riferimento all'interfaccia Strategy.

### Contro
- Se hai solo un paio di algoritmi e che cambiano raramente, non c'è alcun vero motivo per complicare eccessivamente il programma con nuove classi e interfacce che accompagnano il modello.
- I client devono essere consapevoli delle differenze tra le strategie per essere in grado di selezionarne una adeguata.
- Molti linguaggi di programmazione moderni hanno un supporto di tipo funzionale che consente di implementare diverse versioni di un algoritmo all'interno di un insieme di **funzioni anonime**. Quindi potresti usare queste funzioni esattamente come avresti usato gli oggetti strategici, ma senza gonfiare il tuo codice con classi e interfacce extra.