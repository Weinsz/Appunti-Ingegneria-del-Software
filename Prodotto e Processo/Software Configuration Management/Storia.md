Il Configuration Management nasce negli anni ’50 nell’ambito dell’industria aerospaziale. Alla fine degli anni ’70 inizia ad essere applicato all’ingegneria del software.

L’[[Software Configuration Management|SCM]] consiste in delle pratiche che hanno l’obiettivo di rendere sistematico il processo di sviluppo **tenendo traccia dei cambiamenti** in modo che il prodotto sia in ogni istante in uno stato (configurazione) ben definito.

Dunque l’SCM ci permette di controllare le revisioni degli _**artifact**_ (manufatti) e il risultato di tali revisioni; questo processo è molto utile per la generazione di un prodotto a partire da una configurazione ben determinata.

### Manufatti

Gli _“oggetti”_ di cui si controlla l’**evoluzione** sono detti _**configuration item**_ o manufatti, e generalmente sono file. Se si cambia nome a un file è come eliminarne uno e partire da zero con uno nuovo. 
Originariamente i tool tracciavano i file indipendentemente, senza un senso logico (vale a dire una _configurazione_) comune.

![Definizione di configurazione](https://marcobuster.github.io/sweng/assets/05_configuration-management.png)

Riepilogo:
- anni ’80: strumenti **locali** (SCCS…)
- anni ’90: strumenti client-server **centralizzati** (CVS, subversion…)
- anni ’00: strumenti **distribuiti peer-to-peer** ([[Git|git]], mercurial, bazaar…)

Git nasce da un’esigenza di Linus Torvalds con il kernel Linux.