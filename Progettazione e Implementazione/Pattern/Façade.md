- **Tipologia:** Strutturale
- **Scopo:** Fornisce un'interfaccia semplificata a una libreria, un framework o qualsiasi altro insieme complesso di classi.

> Una façade è un oggetto che fornisce un'interfaccia semplificata a un corpo di codice più ampio, come una libreria di classi.
> - Wikipedia

### Problema

Immagina di dover far funzionare il tuo codice con un ampio insieme di oggetti che appartengono a una libreria o un framework particolare. Normalmente, dovresti inizializzare tutti quegli oggetti, tenere traccia delle dipendenze, eseguire metodi nell'ordine corretto e così via.
Di conseguenza, la logica delle tue classi diventerebbe strettamente accoppiata ai dettagli di implementazione delle classi di terze parti, rendendone difficile la comprensione e la manutenzione.

Una façade è una classe che fornisce una semplice interfaccia a un sottosistema complesso che contiene molte parti mobili. Una façade potrebbe fornire funzionalità limitate rispetto all'utilizzo diretto del sottosistema. Tuttavia include solo quelle funzionalità che interessano davvero ai clienti.


### Pattern

Costruendo un sistema complesso può capitare di dover definire una serie di interfacce molto specifiche e dettagliate per i propri componenti, in modo che questi possano lavorare correttamente in accordo tra di loro.
Il problema sorge però quando un Client, dovendo accedere al sistema, si ritrova costretto a dover interagire direttamente con i sottosistemi che lo compongono, cosa che lo obbliga a sviscerare i funzionamenti interni dello stesso per ottenere un comportamento tutto sommato semplice.

Una soluzione comoda sarebbe quella di avere una _maschera_ o *facciata* che fornisce delle operazioni apparentemente semplici all’utente, ma che in realtà nascondo dietro la logica e la combinazione di diversi metodi.

Lo scopo del pattern **Façade** è allora quello di **fornire un’interfaccia unificata e semplificata a un insieme di interfacce separate**: spesso infatti l’uso comune di un sistema si riduce in un paio di operazioni ottenibili combinando varie funzionalità fornite dal package; invece di richiedere al Client di operare tale composizione facciamo ricadere sulle nostre spalle tale compito costruendo una _classe_ Façade che faccia da _interfaccia standard_ al sistema.

![Facade](https://marcobuster.github.io/sweng/assets/09_facade.png)

Si noti come questo non impedisca al Client di usare anche le funzionalità più complesse, ma metta solo ulteriormente a disposizione un’interfaccia che gli permetta di sfruttare facilmente quelle più frequentemente utilizzate.

Una classe Façade può spesso essere trasformata in un [[Singleton]] poiché nella maggior parte dei casi è sufficiente un singolo oggetto façade.

### Esempi

- Un telecomando fornisce un’interfaccia semplice ai controlli della televisione, permettendo di regolare il volume e cambiare canale con semplicità: aprendo però uno sportellino ecco che ci vengono forniti tutti i comandi più specifici. 
- Come funziona una miniera d'oro? “Bene, i minatori vanno laggiù e scavano l'oro”, si potrebbe pensare. Questo è ciò che credi perché stai usando una semplice interfaccia che la miniera fornisce all'esterno, internamente deve fare molte cose per realizzarlo.
- Quando chiami un negozio per effettuare un ordine telefonico, un operatore è la tua facciata verso tutti i servizi e i reparti del negozio. L'operatore fornisce una semplice interfaccia vocale al sistema di ordinazione, servizio di pagamento e vari metodi di consegna.
- Un altro esempio più tecnico è [[GitFlow]] che ci permette tramite semplici comandi di compiere molte più operazioni insieme, come la creazione di branch, lo switching e il merge.

## Pro e Contro

### Pro
- Puoi isolare il tuo codice dalla complessità di un sottosistema.

### Contro
- Una facciata può diventare un [[Anti-pattern God Class|God Object/Class]] accoppiato a tutte le classi di un'app.


