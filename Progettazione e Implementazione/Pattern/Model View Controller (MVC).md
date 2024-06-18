Spesso nei programmi capita che uno stesso dato sia riportato tramite diverse **viste** all'interno dell'interfaccia utente, ad esempio il colore di un testo potrebbe essere rappresentato contemporaneamente da una terna di valori RGB, dal suo valore esadecimale e da uno slider di colori.

Si tratta di un problema simile a quello del pattern [[Observer]], però non riguarda più un semplice dato ma possibili metodi di interazione tra dati e viste, di conseguenza è una **situazione più complessa.** In generale il problema da risolvere è quello di avere modi differenti di rappresentare la medesima **informazione condivisa**, che viene replicata più volte per dare all’utente diversi modi con cui visualizzarla.
La condivisione di un medesimo valore porta però con sé un problema: se tale dato viene modificato dall’utente interagendo con una delle viste è necessario che tale **modifica venga propagata a tutte le altre viste** in modo da mantenere l’informazione **coerente**.

Si ha dunque bisogno di un **framework** che ci permetta di mantenere un’informazione condivisa in modo efficiente e pulito e che permetta di rappresentarla facilmente sotto diversi punti di vista. La soluzione più banale potrebbe essere quella di fare in modo che le viste comunichino direttamente i cambiamenti del dato l’una con l’altra, ma questo approccio si rivela immediatamente impraticabile. 

Il pattern **Model View Controller** (MVC) propone invece di suddividere la gestione del dato e dell’interazione con l’utente in tre tipologie di classi:
- **Model**: un’unica classe contenente lo **stato condiviso**; si tratta dell’unico depositario dell’informazione con cui tutte le viste dovranno comunicare per aggiornare i dati mostrati.
- **View**: una serie di classi che costituiscono l’**interfaccia utente**; esse mostrano il dato secondo il loro specifico punto di vista e permettono all’utente di interagire con l’applicazione.
- **Controller**: ciascuna vista possiede infine una classe di controllo collegata che si occupa della **logica dell’applicazione**; ogni volta che l’utente interagisce con una vista tale interazione viene passata al relativo Controller, che si occuperà di rispondere all’input eventualmente **modificando lo stato condiviso** nel Model.

Si ha quindi una suddivisione dell’applicazione in tre tipi di componenti differenti che cooperano tra di loro **senza però essere _strettamente_ dipendenti** l’uno dall’altro. Un tipico ciclo di interazione tra le tre componenti funziona infatti come mostrato in figura:

![MVC](https://marcobuster.github.io/sweng/assets/09_model-view-controller.png)

1. Una View riceve un'interazione dall'utente e comunica tale evento al proprio Controller;
2. Il Controller gestisce l'interazione e se essa richiede un cambiamento dello stato comune chiede al Model di modificare il suo contenuto;
3. Il Controller aggiorna il dato mostrato dalla View ad esso associata prima ancora che il modello sia cambiato;
4. Il Model, ricevuta la richiesta, si aggiorna e notifica **tutte** le View del cambiamento: così esso non avrà effetto solo nella vista che ha ricevuto l'input bensì in tutte;
5. Le View ricevono la comunicazione del cambiamento del Model e aggiornano la propria informazione mostrata, andando a recuperare il dato aggiornato dal Model (politica **pull**).

Questo modello di interazione circolare permette di separare l’**interfaccia utente** (_view_) dall’**interfaccia dello stato comune** (_model_) e dalla **logica del cambiamento di stato** (_controller_): grazie alla mediazione del Controller le View non hanno bisogno di conoscere direttamente la struttura dei dati contenuti nel Model, cosa che ci permette di riutilizzare le stesse View, e dunque le stesse interfacce utente, per dati diversi (es. una casella di testo è una View e non dipende dal dato che ci si inserisce).

Inoltre è interessante notare come un Controller potrebbe voler comunicare dei _cambiamenti virtuali_ alla View da cui è partito un input prima ancora che al Model venga chiesta un eventuale modifica dello stato. Nel caso ci siano errori nell’input inserito dall’utente, infatti, esso va informato in qualche modo: il Controller non cambierà dunque lo stato condiviso ma solo lo stato dalla relativa View in modo da mostrare un qualche messaggio d’errore. Similmente, se i dati inseriti sono già presenti nel Model (cosa che il Controller non può sapere a priori), lo stesso Model potrebbe avvisare il Controller di tale evenienza al momento della richiesta di cambiamento: esso dovrà dunque nuovamente notificare l’utente che l’inserimento dei dati non è andato a buon fine aggiornando la propria View.

Si analizza ora un altro aspetto: nell’insieme dei meccanismi che realizzano il **pattern Model View Controller** si possono riscontrare una serie di altri pattern trattati. Per agevolare la comprensione del funzionamento di questo nuovo “mega-pattern”, vediamo quindi quali sono i pattern utilizzati al suo interno:
- [[Observer]], poiché _le View sono Observer del Model_: ogni vista si registra come Observer del Model in modo che quest’ultimo, in pieno stile **Observable**, le notifichi dei suoi cambiamenti di stato. Spesso la strategia di aggiornamento delle viste è quella **[[Observer#^89e961|pull]]**; questo permette infatti di memorizzare nello stesso Model i dati di diverse View. 
  Va inoltre fatto notare che se l’interfaccia esposta dalle View è un’_interfaccia a eventi_, come per esempio un’interfaccia grafica (es. un click sullo schermo genera un evento), _anche la comunicazione tra View e Controller può avvenire tramite il pattern Observer_: ciascun Controller si registra infatti come Observer degli eventi che avvengono sulla View.
- [[Strategy]], poiché _i Controller sono Strategy per le View_: ad ogni vista è collegato uno e un solo Controller che regola come la vista reagisca agli input dell’utente; i Controller possono essere visti come strategie di gestione degli eventi generati dalle viste. 
  Poiché le viste sono componenti sostanzialmente “stupidi” che risolvono le interazioni dell’utente **delegando** al proprio Controller la loro gestione, questo approccio permette di gestire viste identiche in modi diversi semplicemente cambiando il Controller ad esse associato; in questo modo è possibile, per esempio, rendere una casella di testo read-only oppure modificabile senza modificare in alcun modo la classe della relativa vista e rispettando così l’**Open-Close Principle**.
- [[Composite]], poiché _le View sono spesso composte da più Component_: quando le View rappresentano GUI, esse sono spesso realizzate componendo diversi elementi tra di loro (es. aree di testo, bottoni...). Per questo motivo è spesso prevalente il pattern Composite nella loro implementazione, utile specialmente per quanto riguarda la creazione su schermo dell’interfaccia, che viene disegnata pezzo per pezzo.

In conclusione, il **Model** è in grado di interagire con tutte le viste che l’osservano tramite un unico comando (_update_), mentre le View comunicano con il Model passando attraverso il Controller, che fa da una sorta di "[[Adapter]]" tra i due. Questo permette allo stesso dato di avere interfacce disomogenee senza alcun tipo di problema riguardante la coerenza dello stesso.

Tuttavia, il problema principale del pattern **MVC** è la **dipendenza circolare tra le tre componenti**: le view comunicano ai rispettivi controller gli eventi, questi li elaborano e aggiornano il modello il quale a sua volta avvisa le view dei cambiamenti di stato. Questa struttura fortemente interconnessa rende **difficoltoso lo sviluppo e il testing** in quanto **non esiste un chiaro punto da cui partire** a costruire: si potrebbe pensare di fare mocking delle view e iniziare a sviluppare il resto, ma questo approccio porta comunque a una serie di inutili complicazioni; bisogna inoltre considerare che il testing delle view è spesso particolarmente complesso dato che coinvolge varie funzioni di librerie diverse. 
In particolare questo modello è molto utilizzato per lo sviluppo di GUI quindi la quantità di aspetti da testare e funzionalità interconnesse è davvero elevata.

Un altro problema di questo pattern è che la View e il Controller dipendono dall’interfaccia, ad esempio nel caso in cui si sfrutti la libreria JavaFX sia View che Controller dipenderanno da essa, e quindi nel momento in cui la libreria venga sostituita con un'altra sarà necessario mettere mano alla maggior parte delle classi dell’applicazione.

Per ovviare a questo problema si decide spesso di spezzare il circolo vizioso di Model, View e Controller modificando lievemente le rispettive dipendenze, col pattern [[Model View Presenter (MVP)]].



