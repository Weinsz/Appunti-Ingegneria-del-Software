Nella programmazione OOP, un oggetto God (a volte chiamato anche oggetto onnisciente) è un oggetto che fa riferimento a un gran numero di tipi distinti, ha troppi metodi non correlati o non categorizzati, o una combinazione di entrambi. 
**God Class/Object** è un esempio di **anti-pattern** e **code smell**.

Una tecnica di programmazione comune consiste nel separare un grande problema in diversi problemi più piccoli (**divide et impera**) e creare soluzioni per ciascuno di essi. Una volta risolti i problemi minori, il grande problema nel suo insieme è stato risolto. Pertanto un dato oggetto per un piccolo problema deve solo conoscere sé stesso. Allo stesso modo, c'è solo un insieme di problemi che un oggetto deve risolvere: i propri problemi. Ciò segue anche il principio [[Conoscenze preliminari#^62f6b3|Single Responsibility]].

Al contrario, un programma che utilizza un God Object/Class non segue questo approccio. 
La maggior parte delle funzionalità complessive è codificata in un singolo oggetto _onnisciente_, che conserva la maggior parte delle informazioni sull'intero programma e fornisce anche la maggior parte dei metodi per manipolare questi dati.

Poiché questo oggetto contiene così tanti dati e richiede così tanti metodi, il suo ruolo nel programma diventa **divino** (onnisciente e onnicomprensivo). Invece di oggetti nel programma che comunicano direttamente tra loro, gli altri oggetti all'interno del programma si affidano all'unico oggetto divino per la maggior parte delle loro informazioni e interazioni. 
Poiché questo oggetto è **strettamente accoppiato** a (referenziato da) gran parte dell'altro codice, la **manutenzione diventa più difficile**.
Le modifiche apportate all'oggetto a beneficio di una funzione, possono avere effetti indesiderati su altre non correlate.
 
Un oggetto God è l'analogo orientato agli oggetti del mancato utilizzo delle funzioni nei linguaggi di programmazione procedurali, o dell'utilizzo di troppe variabili globali per memorizzare le informazioni sullo stato.

Mentre la creazione di una God Class/Object è generalmente considerata una bad practice, questa tecnica viene occasionalmente utilizzata per ambienti di programmazione ristretti (come i microcontrollori), in cui l'aumento delle prestazioni e la centralizzazione del controllo sono più importanti della manutenibilità e dell'eleganza della programmazione.