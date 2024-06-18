GitFlow è una tecnica di organizzazione dei branch e delle repository che prevede la creazione sia di diversi tipi di branch a vita limitata sia il loro _merge_ guidato, anche da remoto.

Si tratta di una serie di comandi _shell_ che vengono uniti in uno script e percepiti da [[Git]] come un comando interno, data la sua natura. Infatti ogni Git non è altro che un wrapper di una serie di altri programmi che eseguono diverse funzioni.

(È disponibile online una [cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/) che fornisce una panoramica veloce delle principali operazioni e dei comandi di GitFlow.)

I branch e i tipi di branch previsti da GitFlow sono:
- branch main;
- branch develop;
- feature branches;
- release branches;
- hotfix branches.

### `--no-fast-forward`

![GitFlow fast forward](https://marcobuster.github.io/sweng/assets/06_gitflow-feature-ff.png)

Di default, git risolve il merge di due branch con la stessa storia banalmente eseguendo il _fast forward_, ovvero spostando il puntatore del branch di destinazione all’ultimo commit del branch entrante.

In GitFlow è preferibile esplicitamente **disabilitare il fast forward** (con l’opzione `--no-ff`) durante il merge in `develop` in quanto è più facile distinguere il punto di inizio e il punto di fine di una feature.

### Squashing

Usando Git è anche possibile eseguire in fase di merge lo _squashing_ dei commit, ovvero la fusione di tutti i commit del branch entrante in uno solo. Questa operazione è utile per migliorare la leggibilità della history dei commit su branch grossi (come `develop` o `main`) ma il suo uso in GitFlow è opinabile: il prof consiglia di non utilizzarlo, in modo da mantenere i commit originali.

### Limiti

git e GitFlow come sono stati esposti presentano numerosi vincoli, soprattutto se utilizzati in grandi team, tra cui:

- la **mancanza di un sistema di autorizzazione granulare**, ovvero la possibilità di assegnare permessi in modo specifico e mirato a diverse funzionalità o risorse. Inoltre, non esiste una distinzione tra diversi livelli di accesso, quindi o si ha accesso completo a tutte le funzionalità o non si ha accesso a niente;
- l’**assenza di [[Tecniche di review|code review]]**, ovvero il processo di revisione del codice sorgente da parte di altri dev prima che venga integrato nella codebase;
- la **mancanza di un sistema di comunicazione tra chi propone una modifica e i reviewer**: git di per sé non mette a disposizione un sistema per agevolare la comunicazione tra chi sviluppa una feature o una modifica e chi si dovrà occupare di revisionarla.

Questi limiti vengono risolti da sovrastrutture che si basano su Git, come GitHub e le istanze di GitLab.

### Git request-pull

Il tool `git request-pull` è un comando di git che serve per generare una proposta di modifiche a un repository tramite una mailing list dopo aver reso pubblici i propri commit su un server. Il comando crea un messaggio di posta elettronica che chiede al maintainer del repository di “pullare” le modifiche, ovvero di integrarle nella codebase. 

Oggi, questa pratica è stata in molti progetti sostituita dalle **pull request**, che sono richieste di integrazione delle modifiche presentate attraverso un’interfaccia web. Le pull request offrono una serie di vantaggi rispetto alle richieste via email, come una maggiore trasparenza del processo di integrazione, una maggiore efficienza e facilità di utilizzo.

Per esempio, i contributori Linux usano questo strumento per chiedere a Linus Torvalds di unire le modifiche nella sua versione. L’output generato mostra file per file le modifiche fatte e i commenti dei commit creati, raggruppati per autore.

Questo modello è un metodo basilare per risolvere i problemi di integrazione. È un sistema _peer to peer_, quindi troppo limitato nei grossi progetti [[Open Source|Open Source]] rispetto alle pull request proposte dai [[Hosting centralizzato|sistemi semi-centralizzati]] spiegati in seguito.