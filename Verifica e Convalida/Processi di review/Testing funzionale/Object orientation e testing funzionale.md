Essendo il [[Testing funzionale]] un approccio **black box** che ragiona sulle **funzionalità** e non sui dettagli implementativi, l’introduzione del paradigma a oggetti **non dovrebbe cambiare nulla** per quanto riguarda il testing funzionale. 
Se questa affermazione è vera per quanto riguarda la verifica di **singole unità funzionali**, lo stesso non si può dire nel caso di **test di integrazione**.

Nei **linguaggi procedurali** i test di integrazione sono infatti scritti secondo logiche alternativamente **bottom-up** o **top-down**: esiste cioè un punto di partenza dal quale partire ad aggregare le componenti, seguendo cioè una qualche forma di **albero di decomposizione** del programma.

Per quanto riguarda la **programmazione a oggetti** invece la situazione è **molto più caotica**: in generale **non esiste la struttura gerarchica** che possa guidare l'integrazione delle unità; le relazioni tra le classi sono spesso **cicliche e non gerarchiche** (tranne per l’*ereditarietà*, che è la relazione meno interessante quando si vuole comporre per risolvere una certa funzionalità), in una serie di **interdipendenze** che rendono **difficoltoso individuare un punto** da cui partire a integrare.

Relazioni interessanti in questa fase sono infatti **associazioni, aggregazioni o dipendenze**, ma rendono complicato identificare il **sottoinsieme di classi da testare**. 
Per fare ciò si possono comunque utilizzare alcuni strumenti già visti:
- si può partire dai diagrammi degli **[[Use case diagram|use cases e scenari]]** per testare i componenti citati;
- si possono osservare i **[[Sequence diagram]]** per testare le classi protagoniste delle interazioni a scambio di messaggi descritte;
- si possono infine usare gli **[[State diagram]]** nella modalità già descritte.