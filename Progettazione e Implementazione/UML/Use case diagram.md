### Concetto e struttura

I **diagrammi dei casi d'uso** rappresentano l'astrazione di un insieme di **scenari** d'uso tra loro correlati.
Essi adottano un linguaggio che verte alla risoluzione di esigenze comunicative tramite un lessico potenzialmente meno tecnico, che evolve durante il [[Processo di produzione del software|processo di sviluppo]]. Tale natura *informale* e più semplice li rende ottimi mezzi di comunicazione col cliente.

Possono essere utilizzati ad esempio per:
- esplicitare **differenti modalità** di fare un compito;
- stabilire quale dovrebbe essere la **normale interazione nello scenario** e le eccezioni che possono verificarsi.

Infatti, ogni **scenario** è corredato di:
- **pre e post-condizioni** da rispettare;
- **flusso di esecuzione** da percorrere in condizioni normali;
- eventuali **eccezioni** e loro possibili trattamenti.

L'evoluzione di questo tipo di diagramma dipende dall'evoluzione del progetto, infatti in prima battuta potrebbe mostrare cosa avviene durante l'interazione tra utente e sistema e progredendo nel tempo il diagramma diventerà più dettagliato, andando a rappresentare gli incarichi dei diversi componenti che comunicano tra loro per compiere le operazioni richieste.

Infine, parte della versatilità degli **Use Case diagrams** risiede nella loro capacità di collegarsi eventualmente ad altri tipi di diagrammi ([[Sequence diagram]], [[Activity diagram]], ecc.) che possono essere impiegati per descriverne in modo più approfondito il flusso.


### Scenari

I componenti di ogni scenario sono utili soprattutto nella **raccolta dei requisiti** e si dividono in:
- **Attori**
- **Casi d’uso**

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/afcab135a1e991f05d66bc9c0bde49102d62d909.svg)]

In generale il _collegamento_ tra un attore e un caso d’uso rappresenta una **relazione di partecipazione**, ad esempio “Questo attore partecipa a questo caso d’uso”.

L’interazione può comunque essere denominata e sono contemplati anche collegamenti fra un caso d’uso e un altro.


### Identificazione degli attori

Gli **attori** sono delle **entità esterne al sistema** ma con cui **interagiscono** fungendo da **fonte o destinatario** di informazioni. Inoltre, quando si parla di attori non ci si riferisce a persone fisiche, ma a **ruoli** da essi compiuti, un altro sistema o anche una periferica hw. 
Va quindi notato che **una persona può ricoprire diversi ruoli contemporaneamente** e quindi rappresentare più di un attore alla volta.

Ci sono due attori particolari:
1. **attore primario**: colui che avvia l’interazione con lo use case.
2. **attore beneficiario**: colui che trae beneficio dall’interazione con lo use case, ovvero chi è **interessato** a tale funzionalità. 

Gli altri attori possono cambiare, ma **il beneficiario rimarrà lo stesso** probabilmente.


### Identificazione degli use case

Il miglior modo di identificare i casi d’uso è interrogarsi su due fronti:
- **sistema**: _“quali funzionalità si desidera che il sistema possieda?”_;
- **attori beneficiari**: _“cosa vogliono?”_, _“come agiscono?”_, _“perché si interfacciano col sistema?”_ e _“cosa si aspettano?”_.

### Associazioni / Relazioni

Successivamente è fondamentale creare le **relazioni tra le figure individuate** facendo molta attenzione, poiché da esse dipenderà la **comprensione** e lo **sviluppo** del progetto. 
I diagrammi [[UML]] possono essere usati per basare la struttura del codice di sviluppo o addirittura creare il software in maniera automatica partendo da essi.

Ogni diagramma dei casi d’uso deve seguire due convenzioni per quanto riguarda le associazioni:

> Ogni attore deve avere almeno un’interazione con un caso d’uso.

Un attore senza alcuna associazione con un caso d’uso sarebbe **impossibilitato a interagire** col sistema e **non avrebbe alcun senso rappresentarlo** nel diagramma.

> Ogni caso d’uso deve essere associato ad almeno un attore.

Un caso d’uso che non coinvolge alcun attore è un caso d’uso che, per definizione, non ha senso di esistere, poiché nessuno è in grado di interagirci.


#### Relazioni use case - use case

Esistono due tipologie di relazioni tra use case:
1. **Inclusione (_include_)**: relazione che esprime il predicato _“far parte di”_, chi include conosce sempre gli inclusi, ma non viceversa (la parte inclusa _deve_ essere eseguita). Viene utilizzata per **fattorizzare** una serie di spiegazioni di comportamento comuni a diversi use cases.

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/9049e55f896d3746fa4ee1119b14dc1c48b7987b.svg)]

2. **Estensione (_extend_)**: relazione che viene utilizzata per rappresentare casi eccezionali che specificano comportamenti particolari in alcuni use case.

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/70b17e60734118c3bede0d914c0eeb7d11897599.svg)]


#### Generalizzazione

L’associazione di **generalizzazione** rappresenta un particolare tipo di relazione, applicabile sia a una coppia _attore - attore_ che a una coppia _use case - use case_.

La sua semantica dipende dal contesto a cui viene applicata:
- **tra attori**: permette di esplicitare eventuali relazioni tra ruoli. Ad esempio un ruolo potrebbe includerne un altro.
- **tra use case**: la semantica è simile all’_extend_, ma senza punti d’estensione. Infatti, alcune parti della descrizione vengono _ereditate_ e altre vengono _sostituite_. Non si applica il [[Conoscenze preliminari#^16f5b7|principio della Liskov]] (questa generalizzazione è deprecata da UML 2.0).


### Esempi

Nel seguente diagramma:

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/6ae0fab45e2176cb7131b443818a99126dec850c.svg)]
l’attore _Book Borrower_ è associato alle seguenti operazioni:
- prendere in prestito un libro;
- chiedere l’estensione del prestito di un libro.

In entrambi i casi, il bibliotecario deve controllare l’esistenza di una richiesta di prenotazione per il libro.

Il prossimo diagramma è differente:

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/77adda9f6be933ea84bf1dfed03117429320c9ac.svg)](https://marcobuster.github.io/sweng/mdbook-plantuml-img/77adda9f6be933ea84bf1dfed03117429320c9ac.svg)

_rifiuta il prestito_ può essere l’**estensione** di un comportamento normale come _prendi in prestito il libro_. In quest’ultimo ci sono dei **punti di estensione** in cui vengono fatti dei controlli, come la verifica dello stato di prestito del libro o dell’identità del richiedente.