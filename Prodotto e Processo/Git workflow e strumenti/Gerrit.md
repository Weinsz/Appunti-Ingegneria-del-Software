Gerrit (prima Mondrian) è un **sistema di [[Tecniche di review|review del codice]]** sviluppato internamente da Google per gestire i suoi progetti [[Open Source]], ormai troppo grandi (es. Android). Nasce dal numero troppo elevato di **pull-request**, data la grande partecipazione al progetto, e si basa sul concetto di **_peer review_**: tutti i dev sono autorizzati a fare review delle proposte di modifica di qualsiasi parte del codice.

Nel processo di review di Gerrit i **developer** possono sottoporre proposte di cambiamento usando un sistema di **patch** che descrive le modifiche apportate al codice. I **reviewer**, cioè gli altri dev del progetto, possono quindi esaminare le patch e decidere se accettarle o meno. Una volta che una patch ha ricevuto un numero sufficiente di review positive, viene automaticamente integrata nel **repository principale authoritative** in cui tutti hanno accesso **in sola lettura**.

Gerrit obbliga a strutturare le **modifiche** proposte non come una storia di commit ma come un **unico commit** (change set) al momento dell'accettazione. Ciò significa che tutte le modifiche apportate devono essere fuse in un unico commit (dietro le quinte [[Git]] usa gli *amend*), in modo da rendere più facile la gestione del repo e per evitare la nascita di troppi rami. 
Al momento della **review** invece le modifiche restano separate in versioni singole, cioè ogni modifica viene presentata come un commit separato, con storia dunque, in modo che i reviewer possano esaminarle più agevolmente.

Due **figure importanti** devono fare parte di questo processo: 
- **verifier**
- **approver**

### Verifier

Strumento/processo che viene usato in Gerrit per verificare che le modifiche proposte siano corrette e funzionino come dovrebbero. Nello specifico, il **verifier** scarica la patch, la compila, esegue i test e controlla che ci siano tutte le funzioni necessarie. Se il verifier rileva dei problemi può segnalarli al team di sviluppo affinché vengano corretti prima che la patch venga accettata.

Si tratta di un processo semplice, dunque può essere anche automatizzato o eseguito da utenti meno esperti o riconosciuti. Una volta terminato il proprio processo, il verifier approva le modifiche, votandole positivamente. Solitamente sono necessari 1 o 2 voti per procedere.

### Approver

Una volta verificata, una proposta di modifiche deve essere anche **approvata**. L'**approver**, che dovrà avere una certa esperienza, dato che non si tratta più di un lavoro meccanico bensì "filosofico", deve dare la risposta alle seguenti **domande riguardo la proposta di modifiche**:
- è valida per lo scopo del progetto?
- è valida per l'architettura del progetto?
- introduce nuove falle nel design che potrebbero causare problemi in futuro?
- segue le best practices stabilite dal progetto?
- è un buon modo per implementare la propria funzione?
- introduce rischi per la sicurezza o la stabilità?

Se l’approver ritiene che la proposta di modifiche sia **valida**, può approvarla scrivendo **“LGTM”** (acronimo di _“Looks Good To Me”_) nei commenti della pull request.

Esiste poi una gerarchia di approver, data dalla loro esperienza e contributo, i cui voti avranno valori diversi; in questo modo è possibile fare una **miglior review distribuita** (ad esempio se le modifiche riguardano l’interfaccia grafica, i voti di un esperto di interfacce grafiche avranno un peso maggiore di un dev back-end).

### Architettura

![Gerrit](https://marcobuster.github.io/sweng/assets/06_gerrit.png)

L'**architettura** di Gerrit è composta da **2 repository**:
1. **Authoritative Repository**: repo in cui vi è SOLO il **diritto di lettura dall'esterno** (*fetch*), mentre è presente il **diritto di scrittura SOLO dall'interno** (*submit*) da parte dell'altro repo;
2. **Pending Changes**: repo in cui i **developer** hanno SOLO il **diritto in scrittura** (*push*), mentre i **reviewer** hanno **diritti speciali** che permettono loro di scaricare le modifiche (*fetch*), valutarle e commentarle (*approve*).

I developer inviano delle modifiche al repo di pending changes, da cui i reviewer faranno tutte le verifiche e valuteranno il lavoro proposto. Poi, una volta che una patch raggiunge un certe numero di valutazioni positive, verrà spostata/inviata al repo principale authoritative, compilando e ricontrollando tutto automaticamente, e i dev potranno vedere le nuove modifiche aggiunte.