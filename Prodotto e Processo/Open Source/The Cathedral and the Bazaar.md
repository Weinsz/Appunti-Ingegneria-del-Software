Raymond propone nel suo [articolo](http://www.catb.org/~esr/writings/cathedral-bazaar/cathedral-bazaar/) due immagini per descrivere i due mondi contrapposti **closed-source** e **open-source**:
- la **cattedrale** (closed-source): ambiente molto gerarchizzato e legato al progetto iniziale di un unico "architetto" responsabile dei lavori;
- il **bazaar** (open-source): ambiente più anarchico possibile, in cui ognuno lavora per sé e costruisce espandendo ciò che gli altri hanno già fatto.

Entrambe le costruzioni sono attraenti ma sono legate a modi di pensare la progettazione/costruzione **totalmente opposti**.

### Vita e vantaggi di un progetto open-source

Nell’articolo Raymond prosegue a descrivere **come nasce** un progetto open-source, esordendo con la seguente citazione:

> Ogni buon lavoro software inizia dalla frenesia personale di un singolo sviluppatore.

Si delinea dunque la seguente timeline di un progetto open source:
1. Un dev ha un problema e vuole risolverlo sviluppando un programma
2. Il dev chiede ad amici o colleghi cosa sanno sull'argomento: alcuni hanno lo stesso problema o simili, ma nessuno ha soluzioni
3. Le persone interessate cominciano a scambiarsi opinioni e conoscenze a riguardo
4. Coloro che intendono spendere delle risorse (tempo libero) per risolvere il problema danno il via a un progetto informale
5. I membri del progetto lavorano sul problema finché non ottengono risultati presentabili.
   Fino a qui però il progetto non è ancora considerabile open-source dato che vi lavora solo una piccola cerchia ristretta di conoscenti: il vero progetto open ha inizio quando **viene messo online il codice sorgente**, a disposizione di tutti.
6. Si pubblica quindi il lavoro online e arrivano i primi suggerimenti esterni al gruppo: questi saranno tanto più frequenti quanto più il progetto presenterà errori, in quanto la comunità sarà motivata a risolverli, essendo composta primariamente da altri dev
7. Si crea interazione tra vecchi e nuovi membri
8. Nuove informazioni e competenze vengono acquisite. Si ritorna al punto 5.

Raymond continua esponendo alcune delle caratteristiche e vantaggi dei progetti open-source, primo fra tutti il fatto che:

> Se dai a tutti il codice sorgente, ognuno di essi diventa un tuo ingegnere.

dove con questo si intende che la possibilità di vedere e commentare il codice permette a utenti esperti di **suggerire modifiche** e prendere parte attiva allo sviluppo. Talvolta si tende però a pensare che un progetto di questo tipo sia destinato unicamente ad altri informatici, ma ciò non è affatto vero: tante attività utili a portare avanti un progetto open-source non richiedono necessariamente competenze informatiche, come per esempio la segnalazione di bug o la moderazione di contenuti nella comunità.

A tal proposito, quanto segue è importante:

> Se ci sono abbastanza occhi (che cercano errori), gli errori diventano di poco conto.

Più sono le persone che controllano e leggono il codice, più sarà probabile trovare gli errori al suo interno. Questi poi possono essere corretti più facilmente grazie al supporto della community di dev, conoscendo magari già una soluzione.
L’accento posto sulla community viene ulteriormente rimarcato dal valore attribuito ai **beta-tester**, che in un progetto open-source rappresentano chiunque utilizzi l’applicazione in qualsiasi suo stadio, vista la sua estrema malleabilità

> Se tratti i tuoi beta-tester come se fossero la tua risorsa più importante, essi risponderanno diventando la tua risorsa più importante

Per mantenere attiva la community di dev è però necessario un costante **monitoraggio** e **cura**. 
Per permettere al progetto open-source di sopravvivere anche quando l’interesse dei creatori originali si è spento è fondamentale passarne il controllo a qualcuno di fidato e competente:

> Quando hai perso interesse in un programma, l’ultimo tuo dovere è passarlo a un successore competente.

Spesso questo passaggio di testimone non viene fatto e il **progetto muore**: occorre invece trovare qualcuno di interessato allo sviluppo, anche perché un programma in uso dovrà necessariamente cambiare ed evolvere in futuro.

### Confronto tra modelli

Per capire meglio i concetti fondamentali del mondo open-source, segue confronto tra lo stesso e i metodi di sviluppo tradizionale e agile nel riguardo di svariati concetti:

| Concetto                           | Tradizionale                                                                                     | Agile                                                                                                                                                 | Open-source                                                                                                                          |
| ---------------------------------- | ------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| __Documentazione__                 | La documentazione è enfatizzata come strumento di controllo di qualità e gestione.               | La [[Documentazione]] non è importante.                                                                                                               | Tutti i manufatti di sviluppo sono disponibili a chiunque, compresi codice e docs.                                                   |
| __Requisiti__                      | Gli analisti traducono le necessità dell'utente in specifiche sw.                                | [[Cliente sul posto\|Gli utenti fanno parte del team]].                                                                                               | Gli sviluppatori spesso sono gli stessi utenti.                                                                                      |
| __Assegnamento dello staff__       | Gli sviluppatori sono assegnati ad un unico progetto.                                            | Gli sviluppatori sono assegnati ad un unico progetto.                                                                                                 | Gli sviluppatori tipicamente lavorano su più progetti con diversi livelli di partecipazione (_impossibile pianificare lo sviluppo_). |
| __Revisione del codice paritaria__ | La revisione del codice tra pari è ampiamente accettata ma raramente effettuata.                 | La [[Pair programming]] introduce una forma di revisione del codice tra pari.                                                                         | La revisione del codice è una necessità ed è praticata quasi universalmente.                                                         |
| __Tempi di rilascio__              | Tante feature in poche release massicce.                                                         | [[Brevi cicli di rilascio \|Tante piccole release incrementali]].                                                                                     | Gerarchia dei tipi di release: **_nightly_** (compilazione giornaliera dal branch *main*), **_development_** e **_stable_.**         |
| __Organizzazione__                 | I team sono gestiti dall'alto.                                                                   | I team sono auto-organizzati.                                                                                                                         | I contributori individuali decidono per sé come organizzare la propria partecipazione.                                               |
| __Testing__                        | Il testing è gestito dallo staff di _Quality Assurance_ (QA), che segue le attività di sviluppo. | Il [[Prodotto e Processo/eXtreme Programming/Tecniche/Testing\|Testing]] è parte integrante dello  sviluppo ([[Test Driven Development (TDD)\|TDD]]). | Il testing e la QA possono essere svolti da tutti gli sviluppatori.                                                                  |
| __Distribuzione del lavoro__       | Parti differenti della codebase sono assegnate a persone differenti.                             | [[Proprietà collettiva\|Chiunque può modificare qualsiasi parte della codebase]].                                                                     | Chiunque può modificare qualsiasi parte della codebase, ma solo i **_committer_** possono rendere ufficiali le modifiche.            |
