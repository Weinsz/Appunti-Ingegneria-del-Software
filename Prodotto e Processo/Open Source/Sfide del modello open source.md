Per via della sua natura il modello di sviluppo open source pone **sfide sconosciute** all'ambiente di sviluppo tradizionale. Prima di affrontare i tool di design e organizzazione del lavoro nati per risolvere questi problemi, ne si dà di seguito un'introduzione.

### Difficile integrazione del software

Si tratta di una vecchia sfida che è enormemente amplificata nell'ambito **FOSS**. Per integrare le nuove feature sviluppate in un sw stabile, diversi modelli avevano costruito le proprie tecniche:
- Nel [[Modello a cascata]] l'integrazione era una fase circoscritta a sé stante.
- A tale struttura rigida si contrappone lo schema **Stabilize & Synchronize** nato in Microsoft: di giorno i dev lavorano sul proprio codice, di cui sono responsabili, e di notte il sw viene ricompilato da zero. La mattina dopo c'erano 2 possibilità:
	- la compilazione falliva e il responsabile veniva trovato e "punito";
	- la compilazione aveva successo, il sw era integrato e quindi nella *versione migliore possibile* (che non è per forza una versione stabile).
- In [[eXtreme Programming (XP)|XP]] l'[[Integrazione continua|integrazione]] veniva eseguita più volte al giorno in modo esclusivo: un solo dev alla volta poteva integrare il proprio lavoro sull’unica macchina di integrazione disponibile. Ciò permetteva di individuare facilmente eventuali problemi di integrazione e risolverli rapidamente.

Come viene organizzata l'integrazione nel mondo open source? Per sua natura, in questo ambito l'[[Integrazione continua|integrazione viene eseguita continuamente]] e senza coordinazione a priori (anche perché il team è sparso): si tratta di **anarchia totale**, con lo svantaggio che da un momento all'altro una grande fetta della codebase potrebbe cambiare in quanto un singolo dev potrebbe integrare mesi e mesi di lavoro tutto insieme. Per fortuna sono nati **strumenti** per contenere questo problema.

### Sfaldamento del team

Nell’open source nascono inoltre problemi nella gestione del team. Occorre decidere come:
1. comunicare
2. tenersi uniti
3. coordinarsi
4. ottenere nuove collaborazioni

Per comunicare si utilizza di solito **internet**: si potrebbe dire che **senza internet non potrebbe esistere il concetto stesso di open source**. 

Si utilizzano spesso dei **forum** o simili per organizzare il lavoro, in modo da tenere la **community unita** e rispondere ai dubbi dei nuovi utenti.

Per quanto riguarda il coordinamento del lavoro sono nati strumenti per la sincronizzazione del lavoro e **versioning** di codice, come [[Git]]. Per le documentazioni inizialmente si sfruttavano le **wiki**, anche se ora sono poco usate (sia GitHub sia GitLab le supportano però) in favore di siti compilati contenenti la doc del sw. Questi siti si chiamano **Pages** e per realizzarli si sfruttano tool basati su Markdown, potendo fare anche qui versioning.

Deve poi essere facile poter compilare il codice e ricreare l’ambiente di sviluppo omogeneo per tutti. Si utilizzano quindi strumenti di **[[Build automation|automatizzazione delle build]]** (es. **Makefile**) in modo che chiunque voglia partecipare possa farlo indipendentemente dalla propria configurazione sw e hw.

È infine importante **educare i reporter dei bug** e avere un sistema per organizzare per le **[[Bug tracking|segnalazioni di errori]]**: il sistema dovrebbe essere accessibile a tutti in modo da evitare segnalazioni duplicate e consentire una facile organizzazione delle stesse. Si anticipa che anche una segnalazione d’errore avrà il suo ciclo di vita.