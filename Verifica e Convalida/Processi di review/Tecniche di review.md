Si sono viste tecniche più o meno **automatiche** per la ricerca di errori, che **stimolano** il programma con specifici input o ne **analizzano il codice** per individuare potenziali *anomalie*. 

Tuttavia, alcuni tipi di errori non possono essere rilevati con questi metodi: si tratta soprattutto di errori legati a **incomprensione delle specifiche**. Del resto, attività come il [[Verifica e Convalida/Analisi statica/Testing|Testing]] richiedono che il programmatore fornisca l'output *corretto* che si aspetta dal programma che viene confrontato con quello *effettivo* per scovare possibili differenze:

> Se chi scrive il codice non comprende in prima istanza **cosa** dovrebbe fare il suo sw non c'è modo di individuare l'errore.

Perciò molto spesso il codice viene sottoposto ad un'**attività di review**, in cui una persona ne analizza la struttura e il funzionamento: egli sarà chiaramente in grado di cogliere una serie di **errori semantici** che sfuggono alla comprensione dei **tool automatici di test**.
Spesso questo compito viene svolto da un **team di testing**, separato dal **team di sviluppo**: ciò promuove non solo l'effettiva ricerca di errori (mentre i dev avrebbero tutto l'interesse di non trovarne nessuno), ma sottopone il sw a uno **sguardo esterno** più critico e imparziale.

Anche per la **review** esistono una serie di **tecniche**:
- [[Bebugging]]
- [[Analisi mutazionale]]
- [[Object oriented testing]]
- [[Testing funzionale]]
- [[Software inspection]]
- [[Modelli statistici]]
- [[Debugging]]