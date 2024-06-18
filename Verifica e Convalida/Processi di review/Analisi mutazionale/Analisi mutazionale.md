Un'evoluzione del [[Bebugging]] è l'**analisi mutazionale**.
Dato un programma $P$ e un test $T$, viene generato un insieme di programmi $\Pi$ **simili** (non uguali) al programma $P$ in esame, detti **mutanti**.
Si esegue poi il test $T$ su ciascun mutante:
- se $P$ è corretto **i programmi in $\Pi$ devono essere sbagliati**, ovvero devono produrre un **risultato diverso** per almeno un caso di test $t\in T.$ 
- se non fosse così infatti, vorrebbe dire che il programma $P$ non viene opportunamente testato **nell'aspetto in cui si discosta dal mutante che non ha sollevato errori**, per cui non si può essere sicuri della correttezza. Non viene cioè testata la correttezza del programma, ma invece **quanto il test è approfondito**.

Si può dunque **valutare** la capacità di un test di rilevare le differenze introdotte nei mutanti tramite un nuovo **criterio di copertura**, detto [[Criterio di copertura dei mutanti]].

Si vede poi:
- [[Generazione dei mutanti]]
- [[Automazione dell'analisi mutazionale]]