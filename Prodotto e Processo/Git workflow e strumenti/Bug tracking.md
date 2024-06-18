Il bug tracking è stato reso necessario nel mondo [[Open Source]] per via della numerosità dei contributi e dell'elevata probabilità di avere segnalazioni duplicate.

Inoltre, per gestire le **segnalazioni di bug** nell’ambito dello sviluppo open source, esistono diversi strumenti come git-bug, BugZilla, Scarab, GNATS, BugManager e Mantis.

Questi tool guidano l’utente, anche quelli meno esperti, nella segnalazione di bug, creando un **database** che permetterà di **evitare segnalazioni duplicate** semplificandone la visione, l’organizzazione e la comunicazione del lavoro.

### Bug workflow e ciclo di vita

![Bug workflow](https://marcobuster.github.io/sweng/assets/06_bug-workflow.png)

L’obiettivo del bug tracking è avere **più informazioni possibili su ogni bug** in modo da poterli **riprodurre** (un bug non riproducibile potrebbe non dipendere dal software ma dal contesto in cui si trova) e di conseguenza **arrivare a una soluzione**.

**Ogni bug quindi avrà un suo ciclo di vita**, descritto nell’immagine, che potrà intraprendere diversi percorsi. È importante verificare i bug una volta che l’_issue_ è stato aperto, in modo da poter confermare la sua **esistenza** e la **completezza** delle informazioni fornite.

Un _issue_ è una segnalazione relativa ad un **malfunzionamento di una feature** presente all’interno di un progetto di software, oppure una **richiesta di aggiunta** di nuove funzionalità. Gli issue possono essere aperti da qualsiasi membro del team o dalla comunità, e possono essere **risolti o chiusi** da un membro del team responsabile.

Ci sono diversi modi per cui può essere chiuso un bug:

- **duplicate**: quando è stato **già segnalato in precedenza** e quindi non rappresenta un nuovo problema. In questo caso, viene solitamente fatto riferimento al numero del bug originale che ha già ricevuto una **risoluzione**;
- **wontfix**: il bug viene chiuso come **“non risolvibile”** perché o rappresenta una funzionalità voluta dal progetto o è **troppo complesso** da risolvere per essere considerato conveniente farlo dal punto di vista dei progettisti;
- **can’t reproduce**: non è stato possibile riprodurre il bug, ovvero che **non è stato possibile ottenere lo stesso risultato** o il comportamento segnalato dal bug. Ciò può essere dovuto a una mancanza di dettagli o a un errore nella segnalazione del bug stesso;
- **fixed**: il bug è stato fixato;
- **fix verified**: il **fix è stato integrato in una release** passando tutti gli step di verifica.

I tool di bug tracking sono sempre **più integrati negli strumenti di versioning**, quindi il bug viene legato a un commit specifico. 
Da ciò è possibile ricavarne l’evoluzione durante la sua risoluzione in base alle transizioni di stato e ai commenti dei commit. Ovviamente questo processo si complica se saranno presenti diversi rami nel progetto, infatti solitamente **una segnalazione viene chiusa quando il commit che risolve il problema entra a far parte del ramo master**. 
Un ulteriore problema riguarda la **poca compatibilità** tra le fasi della vita di un issue e le operazioni di un tool di versioning. Questo porta a una difficile rappresentazione dello stato del problema.