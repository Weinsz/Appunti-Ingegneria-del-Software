Ora si parla nel concreto di [[eXtreme Programming (XP)]], una tecnica di sviluppo [[Metodologie Agile|Agile]] nata tra fine '90 e inizio 2000 da **Kent Beck**, che la ideò nell'ambito di un **progetto Chrysler**.

### Variabili

Secondo Beck, durante lo sviluppo sw le principali variabili sono:
- **portata**: la quantità di funzionalità da implementare, una varabile delicata dal valore mutevole poiché il numero di funzionalità richieste può cambiare nel corso dello sviluppo;
- **tempo**: il tempo che si può dedicare al progetto;
- **[[Qualità del software|qualità]]**: la qualità del progetto che si vuole ottenere, principalmente relativa a correttezza e affidabilità. Di fatto è una costante perché quando si realizza un progetto si cerca di avere la qualità migliore possibile (sappiamo non essere sempre così nella pratica a causa di compromessi da accettare);
- **costo**: le risorse finanziarie o in termini di personale che si possono impegnare per il progetto.

Queste 4 variabili non sono indipendenti tra loro, influenzandosi l'una con l'altra al mutare di una. Ponendo quindi che la qualità non sia negoziabile, in quanto il sw deve funzionare, si dovrà lavorare sulle altre, specialmente bilanciando costo e tempo.

Nel panorama classico di sviluppo la portata era definita in modo rigido dal cliente, che richiedeva certe funzionalità non negoziabili e pagava lo sviluppatore a progetto completo. 
Con XP si stravolge la prospettiva: **il costo è orario**, il tempo disponibile non è fisso ma pari al tempo richiesto per lo sviluppo e la portata viene ricalcolata durante il progetto, essendo così l'unica variabile a variare effettivamente. 
Si tratta di un **approccio incrementale** che mira ad avere sempre un prodotto consegnabile se il cliente si sente soddisfatto dello sviluppo. Quindi non si fa aspettare il cliente per dargli tutto in una volta sola, ma si consegna volta per volta. Oltre ad alleggerire la pressione sul dev, quest'approccio è utile per 2 motivi:
1. il cliente è certo che il dev si stia dedicando al progetto dato che vede il progetto crescere man mano; inoltre anche [[Cliente sul posto|il cliente fa parte del team]], di conseguenza può accertarsi coi suoi occhi dell'impegno del team.
2. dà la possibilità al cliente di avere qualcosa in mano quando vuole e gli permette di cambiare idea sulla portata e sulle funzionalità richieste in corso d'opera, bandendo la rigidità dei documenti di specifica.

Tutti questi aspetti consentono di creare un rapporto meno conflittuale col cliente, c'è più collaborazione avendolo nel team e, inoltre, si ha un feedback rapido in ogni momento.

### Principi

Confronto tra i fondamenti della filosofia XP e i **principi dell'ingegneria del sw classica**, elencati di seguito:
- **Separazione degli interessi**: separare tempi, responsabilità e moduli, ovvero tutte le varie viste o dimensioni su cui si deve affrontare il problema
- **Astrazione e modularità**: bisogna usare le giuste astrazioni che ci consentono di dominare i problemi complessi (es. i diversi linguaggi di programmazione, di descrizione o vari altri costrutti). Questo aspetto è importante perché più un problema è complesso più è necessario un certo livello di astrazione per rappresentarlo
- **Anticipazione del cambiamento** (_design for change_): in fase di progettazione il dev deve pensare a come potrebbe evolvere il prodotto, rendendo possibile l'eventuale aggiunta di requisiti a cui il cliente magari non aveva neanche pensato; bisogna fare attenzione però, perché spesso questo concetto complica arbitrariamente la progettazione e lo sviluppo, rischiando di far perdere molto tempo su cose che al cliente potrebbero non servire: può essere un’idea migliore partire da qualcosa di semplice ed incrementare man mano
- **Generalità**: per rendere più semplice la modifica ed espansione futura è cruciale scrivere interfacce molto generali ai sistemi che costruiamo
- **Incrementalità**: lo sviluppo avviene incrementalmente
- **Rigore e formalità**: è importante essere rigidi e formali sia nella comunicazione che nella descrizione dei requisiti.

L’XP non è niente di rivoluzionario, infatti non butta via tutti questi principi ma invece ne eredita alcuni e li adatta alle proprie necessità, specialmente la **separazione degli interessi**, che viene data per scontata. L’XP pone pure l’accento su altri aspetti, ovvero:
- **Feedback rapido**: bisogna mantenere un continuo flusso di feedback; questo viene dato dai test, dai colleghi ma anche dal cliente, che dev’essere sempre consultato sullo stato dei lavori. Tra le iniziative che favoriscono un veloce ciclo di feedback c’è lo **standup meeting**, una riunione mattutina in cui ciascuno descrive in poche parole cosa ha fatto il giorno prima e cosa intende fare oggi
- **Presumere la semplicità**: non bisogna complicare senza motivo né il codice, che deve essere scritto con in mente ciò che serve a breve termine e non in un futuro remoto, né le relazioni tra colleghi, che non devono essere eccessivamente gerarchiche (tutti dovrebbero avere compiti molto simili). In generale si dovrebbe semplificare il più possibile in tutti gli ambiti del progetto
- **Accettare il cambiamento**: non ci si deve aspettare che il sw sia immutabile; al contrario, deve essere dato per scontato il concetto di **flessibilità** e **malleabilità**, cioè che il cliente vorrà fare modifiche sia dopo che durante lo sviluppo del prodotto, ma non deve essere nemmeno il primo obiettivo del lavoro. Se ne tiene conto senza perderci troppo tempo
- **Modifica incrementale**: concetto di baby-steps; questa regola si applica però a tutti gli ambiti del progetto, dalla raccolta dei requisiti alla gestione del team: ovvero non bisognerebbe mai aggiungere più di una persona alla volta al gruppo di lavoro, in quanto aggiungerne di più potrebbe portare a passare più tempo a spiegare cose che a sviluppare
- **Lavoro di qualità**: bisogna ovviamente ottenere un buon prodotto, ma per farlo la prospettiva cambia in favore del dev, al quale si deve garantire un ambiente di lavoro sano e un certo grado di benessere; la fidelizzazione dei dev è importante perché meglio stanno e meglio lavoreranno.

I due punti più in contrasto sono il **presumere la semplicità e l’anticipazione del cambiamento**: sembra infatti più previdente pianificare per il futuro e anticipare eventuali cambiamenti, ma talvolta questo può essere controproducente.
### Presumere la semplicità vs anticipazione del cambiamento

XP dà priorità alla semplicità: non si scrive in anticipo codice che si pensa si scriverà in futuro. Questo non significa che non si stia progettando per il futuro, ma solo che non è il primo aspetto da guardare, bensì deve essere la semplicità, cioè fare le cose nel modo più chiaro possibile.

**Non pianificare il futuro sembra rischioso:** secondo uno studio fatto da Bohem nel 1976 (basato anche sull'esperienza personale) viene ipotizzata una curva esponenziale per il costo delle modifiche all'aumento dell'avanzamento del progetto. Più il progetto avanza più è costoso modificarlo, a causa dell'accumulo del **debito tecnico**, motivo per cui sembra necessario accomodare il cambiamento futuro in modo da ridurre tale costo.
Al contrario, XP presuppone una curva logaritmica che tende a un asintoto: passato un certo punto nello sviluppo, il costo per le modifiche non subisce più cambiamenti sensibili. Si suppone che ciò accada grazie al miglioramento dei linguaggi e delle tecniche stesse (come **[[Prodotto e Processo/eXtreme Programming/Tecniche/Refactoring|Refactoring]]**), per cui non ha senso fasciarsi la testa in anticipo in quanto **un codice semplice è relativamente facile da modificare**.

![Curve di costo: XP vs tradizionale](https://marcobuster.github.io/sweng/assets/03_cost-curves.png)

Va considerato che Bohem parlava in realtà di **cost-to-fix**, e non del costo per la modifica in sé. Inoltre la sua statistica era poco affidabile in quanto era stata costruita a partire da **pochi dati**. La curva esponenziale da lui descritta è stata poi ritrattata per accomodare il fatto che se un errore avviene in una fase affligge solo le successive, non le precedenti.

### Figure e responsabilità

Per organizzare il lavoro, **XP** individua **diverse figure** che partecipano allo sviluppo:
- **Cliente**: colui che richiede funzionalità e conosce il dominio applicativo
- **Sviluppatore**: colui che sviluppa concretamente scrivendo codice
- **Manager**: colui che amministra lo sviluppo con uno sguardo generale.

Ciascuna di tali figure ha responsabilità e diritti riassunti nella seguente tabella (manager e cliente sono accorpati perché hanno grossomodo gli stessi compiti nelle tecniche di sviluppo moderne, come in **Scrum**):

| Soggetto            | Ha responsabilità di decidere                                                                                                                                                                                                                 | Ha diritto di                                                                                                                                                                                                                                                                                                                                                   |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Manager/Cliente** | - **portata** del progetto, cioè<br>le funzionalità da realizzare<br>- priorità tra **funzionalità** e loro<br>**business value**<br>- **date dei rilasci**, anche nel caso<br>di release incrementali                                        | - sapere cosa può essere fatto,<br>con quali tempi e costi<br>- vedere **progressi** nel sistema e la sua<br>correttezza, provati dai test da lui <br>definiti (**trasparenza**)<br>- **cambiare idea**, sostituendo<br>funzionalità o cambiandone le priorità<br>a intervalli di tempo fissi<br>(fine del ciclo di sviluppo incrementale)                      |
| **Sviluppatore**    | - **stime** dei tempi per le singole<br>funzionalità (no deadline imposte)<br>- **scelte tecnologiche** e loro<br>conseguenze, ovvero come si<br>realizzano le funzionalità richieste<br>- **pianificazione** dettagliata delle<br>iterazioni | - ricevere dei **requisiti chiari** (casi d'uso)<br>con priorità per le varie funzionalità<br>- **cambiare le stime** dei tempi man<br>mano che il progetto procede <br>e il contesto cambia<br>- identificare **funzionalità pericolose**<br>o troppo **difficili** da realizzare<br>- produrre sw di **qualità**, perciò deve<br>godere di un certo benessere |

**Business value:** valore che assume una feature, dipendente dal costo in termini di difficoltà e dalla sua importanza all'interno del sistema. Questo valore viene sfruttato per decidere in che ordine dedicarsi alle feature da implementare.

Dunque per migliorare la fiducia tra dev e cliente sono necessari due requisiti:
1. un certo grado di **trasparenza** da parte di chi sviluppa, ottenuta dall'uso delle continue release incrementali
2. una certa dose di **pazienza** da parte del cliente, che deve accettare di lasciare al dev la facoltà di decidere come realizzare le feature e di cambiare le prospettive temporali di sviluppo in caso

Inoltre nel team vi è anche la figura del **tracker**, ovvero una persona nel team (non fissa) incaricata di tenere traccia delle problematiche incontrate nell'iterazione. Per fare ciò definisce una **metrica** (es. numero di issue aperti) ragionevole per misurare lo stato del problema in esame, segnando ogni misurazione ad esempio nella lavagna dell'ufficio. Grazie a questa figura tutto il team conosce i problemi principali che sono stati riscontrati durante il progetto, e ad ogni iterazione si cerca di capire in che modo risolverli per migliorare il [[Processo di produzione del software|processo di sviluppo]].

principi