Generalmente nel **testing** gli unici due esiti sono risultato **corretto** o **non corretto** e la metrica è una misura della correttezza del programma. Come già detto, il discriminante delle tecniche di analisi mutazionale è invece il numero di casi di test che forniscono un risultato **diverso** da quello di $P$, indipendentemente dalla **correttezza** (di entrambi).
Trovare errori con queste tecniche (come [[Generazione dei mutanti#^5a042e|HOM]]) misura quindi il **livello di approfondimento dei casi di test**, non la correttezza del programma di partenza. 
Prescindere dalla correttezza dei risultati ha però un aspetto positivo: per eseguire l'[[Analisi mutazionale]] non è necessario conoscere il comportamento corretto del programma, eliminando la necessità di un **oracolo** che ce lo fornisca.
Si può quindi misurare la bontà di un insieme di casi di test **automatizzando la loro creazione**: occorre però vigilare sulla **proliferazione del numero di esecuzioni** da effettuare per completare il test; un caso di test dà infatti origine a $n+1$ esecuzioni, dove $n$ è il *numero di mutanti*.


### Diagramma di flusso dell'automazione

Il seguente diagramma di flusso visualizza quindi l’**attività facilmente automatizzabile** di analisi mutazionale:

![Schema analisi mutazionale](https://marcobuster.github.io/sweng/assets/13_analisi-mutazionale-schema.png)

Questo algoritmo **non garantisce la terminazione** per diversi motivi:
- quando si estrae un caso di test casuale, si ha sempre il rischio di **estrarre lo stesso caso di test**;
- si potrebbe essere **particolarmente sfigati** e non trovare un **caso di test utile** in tempo breve;
- **esistono infinite varianti di programmi funzionalmente identici ma sintatticamente diversi**, ovvero che svolgono la stessa funzione anche se sono scritti in modo diverso: una modifica sintattica potrebbe non avere alcun effetto sul funzionamento del programma (per esempio scambiare `<` con `<=` in un certo algoritmo di ordinamento). In tal caso, *nessun nuovo caso di test permetterebbe di coprire il mutante*, in quanto esso restituirebbe sempre lo **stesso output del programma originale**.

Spesso viene dunque posto un *timeout* sull'algoritmo dipendente sia dal tempo totale dell'esecuzione, sia dal numero di casi di test estratti.

Nel momento in cui si aggiunge il caso di test $t$ e scatta il timeout, si controlla il **numero di mutanti che non si è riusciti a distinguere** (quelli molto simili) in modo da verificare la validità del test; se sono tanti in percentuale, allora il test non è affidabile. In alternativa, è possibile *nascondere* i mutanti, in quanto essendo stati generati casualmente magari la volta successiva non verranno rigenerati. Ciò viene fatto però a patto che non sia richiesta una **copertura totale** (100%). 
Così facendo, è possibile **analizzare programmi quasi identici, che sono funzionalmente uguali ma sintatticamente diversi**, al fine di dimostrarne l'**equivalenza** o scoprire un caso o più in cui questa equivalenza non è valida.