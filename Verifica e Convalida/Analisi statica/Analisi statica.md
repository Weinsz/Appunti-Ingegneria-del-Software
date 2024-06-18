Il testing dell'esecuzione del programma non è però l'unica cosa che possiamo fare per aumentare la fiducia nostra e del cliente nella **correttezza del programma**.
Rimanendo nel **testing strutturale** possiamo fare una analisi più approfondita del codice.

Un'altra importante iniziativa in tal senso è l'**ispezione del codice** del programma tramite varie tecniche, attività che prende il nome di **analisi statica**.
Si è considerato per ora solo il **flusso di controllo**: si possono fare considerazioni sul **flusso dei dati**? Sì, ma necessita di una fase a priori di **analisi statica**.

L'**analisi statica** si basa sull'esame di un **insieme finito di elementi** (*le istruzioni del programma*), contrariamente all'analisi **dinamica** (*testing*) che invece considera un **insieme infinito** (*gli stati delle esecuzioni*). 
L'**analisi statica** è quindi un'attività **meno costosa del testing**, in quanto non soffre del problema dell'**esplosione dello spazio degli stati**.

Considerando solamente il **codice statico** del programma, questa tecnica **non ha la capacità di rilevare anomalie dipendenti da particolari valori assunti dalle variabili a runtime**. Si tratta in ogni caso di un’**attività estremamente utile**, che può aiutare a individuare numerose anomalie e inaccortezze.

Si tratta:
- [[Compilatori]]
- [[Analisi Data Flow]]
- [[Verifica e Convalida/Analisi statica/Testing|Testing]]
- [[Criterio di copertura delle definizioni]], [[Criterio di copertura degli usi]], [[Criterio di copertura dei cammini DU]]
- [[Oltre le variabili]]