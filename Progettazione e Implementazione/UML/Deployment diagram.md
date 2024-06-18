Il **deployment diagram** permette di rappresentare la **dislocazione fisica** delle risorse.  
Più precisamente, specifica la dislocazione fisica delle **istanze dei componenti**.

Il deployment diagram è una **vista statica della configurazione a runtime**, ovvero si rappresenta come sono **posizionati sulle macchine** i diversi componenti utilizzati e come comunicano tra loro.

La conformazione del diagramma è quindi molto simile a quella del [[Component diagram]], ma con qualche differenza:
- i **nodi** del sistema rappresentano **macchine fisiche**;
- i **collegamenti tra nodi** esplicitano le **modalità di comunicazione** tra gli stessi (es. RMI, HTTP).

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/441f547869267d5440cb5910727a73e53a33ccfb.svg)]

Il **deployment diagram** risulta di particolare utilità per il **deployer**, ovvero la figura che si occupa dell’**installazione fisica del sistema**. In questo modo sarà possibile **ottimizzare l’utilizzo trasversale delle risorse** tra le varie componenti del sistema.