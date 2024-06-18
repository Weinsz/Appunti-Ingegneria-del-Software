Questa tecnica mira a testare come i vari sottosistemi del programma **dialoghino e collaborino tra loro**: per **interfacce** non si intendono quelle di Java o le *signature*, ma l'insieme di funzionalità che permettono l'**interoperabilità** dei componenti. Esistono in particolare diversi tipi di interfacce:
- a **invocazione di parametri**;
- a **condivisione di memoria**;
- a **metodi sincroni**;
- a **passaggio di messaggi**.

Le interfacce aderenti a ciascuna categoria possono essere analizzate in modi diversi alla ricerca di anomalie. Gli sbagli più comuni sono per esempio:
- **errori nell'uso dell'interfaccia**, come il passaggio di parametri in ordine o tipo errato, oppure assunzioni sbagliate circa ciò che le funzionalità richiedono (*precondizioni*);
- **errori di tempistica o sincronizzazione** tra componenti.