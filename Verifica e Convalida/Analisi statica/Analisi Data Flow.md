Nata nell'ambito dell'**ottimizzazione dei [[Compilatori|compilatori]]**, in quanto essi per migliorare le proprie performance ricercavano porzioni di codice non raggiungibili e da non compilare.
L'**analisi del flusso di dati** è stata più avanti presa dall'ingegneria del sw per ricercare e **prevenire le cause di errori** simili.
Parlando di **flusso dei dati** si potrebbe pensare a un'**analisi dinamica** come il **testing**, ma è invece **particolarmente significativo** l'insieme dei **controlli statici** che si possono fare sul codice per comprendere come vengono utilizzati i **valori** presenti nel programma.

Si può infatti analizzare *staticamente* il **tipo delle operazioni eseguite su una variabile** e l'**insieme dei legami di compatibilità** tra queste operazioni per determinare se il valore in questione viene usato in maniera **semanticamente sensata** all'interno del codice.

Nello specifico, le **operazioni** che possono essere eseguite **su un dato** sono solamente di tre tipi:
1. ==**d**== (**definizione**): il comando **assegna un valore alla variabile**; anche il **passaggio del dato come parametro** a una funzione che lo modifica è considerata un'operazione di **(ri)definizione**;
2. ==**u**== (**uso**): il comando **legge il contenuto di una variabile**, come per esempio l'espressione sul lato destro di un assegnamento;
3. ==**a**== (**annullamento**): al **termine dell'esecuzione** del comando il valore della variabile **non è significativo/affidabile**. Per esempio, dopo la **dichiarazione senza inizializzazione** di una variabile e **al termine del suo *scope*** il valore è da considerarsi inaffidabile.

> Dal **punto di vista di ciascuna variabile** si può ridurre una **una qualsiasi sequenza d'istruzioni** (*ovvero un cammino sul diagramma di flusso*) a **una sequenza di *definizioni, usi e annullamenti***.

Dopodiché si analizzano:
- [[Regole Data Flow]]
- [[Sequenze Data Flow]]