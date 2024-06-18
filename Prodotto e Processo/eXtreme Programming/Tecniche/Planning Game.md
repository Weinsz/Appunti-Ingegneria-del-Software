Si tratta dell'attività di pianificazione che viene fatta all'inizio di ogni iterazione e serve per congelare il sottoinsieme di requisiti sul quale il team lavorerà per le prossime circa 2 settimane. Questa procedura è posta ai membri del team come un gioco, in modo da alleggerire, almeno apparentemente, la riunione da fare ad inizio iterazione.

Si parte dalle richieste del cliente espresse tramite **user stories**, una versione semplificata degli **[[Use case diagram|use cases]]** di UML. Esse hanno come soggetto sempre un **ruolo specifico** nell'azienda del cliente e descrivono una funzionalità. 
Ogni user story è composta da 3 parti:
1. il **soggetto**, cioè il ruolo dell'utente nell'azienda (può anche essere esterno)
2. l'**azione** che vuole eseguire il soggetto
3. la **motivazione** che spinge il soggetto a portare avanti l'azione descritta

Esempi di user stories:
- Da **bibliotecario**, voglio poter **visualizzare dove si trova** un particolare libro in modo da **poterlo reperire per i clienti.**
- Da **utente** della biblioteca, voglio poter **visualizzare lo stato di un libro** per poterlo prendere in **prestito**.

Lo scopo del planning game è dunque quello di determinare quali **funzionalità** saranno presenti nel **prossimo rilascio** combinando priorità commerciali e valutazioni tecniche: ciò richiede una collaborazione da parte del cliente, che è [[Cliente sul posto|presente sul posto]] al momento della decisione.

### Procedura

![Card user story](https://marcobuster.github.io/sweng/assets/03_user-story-card.png)

Quest’attività di pianificazione si divide fondamentalmente in 3 fasi:
1. Prima dell’inizio del planning game, il cliente compila le **carte**, che sono nient’altro che pezzi di carta volutamente piccoli per impedire di scriverci troppo. Su ogni carta è presente:
    - un **identificativo** numerico;
    - una breve frase che descrive uno **scenario d’uso**;
    - un caso di test che funge da **test d’accettazione** della funzionalità: si tratta in pratica di un paio di esempi (di solito uno positivo e uno negativo) che devono essere soddisfatti per ritenere completa la feature;
    - il valore di business che la funzionalità ha per il cliente.
2. Per ogni carta il team di dev fa dunque una **stima del tempo necessario a realizzarla**: raggiunta una stima comune questa viene scritta sulla carta e servirà per confrontare tale previsione con il tempo effettivamente impiegato, di cui si tiene conto sul suo **retro**.
3. Il manager decide quindi sulla base di queste informazioni **quali carte verranno implementate** durante **prossima iterazione**: per questa operazione prende in considerazione il valore delle feature, le dipendenze tra l’una e l’altra e altri fattori. Se, come dovrebbe essere, le varie funzionalità rappresentate nelle carte sono **indipendenti**, il manager può compiere questa scelta calcolando il **rapporto tra il valore e il tempo stimato** e usarlo per ordinare le carte: tuttavia l’operazione richiede una certa dose di ragionamento e non è mai così meccanica.

### Le stime

Le stime dei tempi vengono fatte dall’intero team in accordo. Tuttavia, esso è composto da **persone diverse** che quindi faranno stime diverse in base all’esperienza e alle proprie capacità. 
È tuttavia importante raggiungere una **stima comune a tutti** in quanto il team si impegna a rispettarla: se viene deciso che il tempo per una data scheda è di qualche ora e questa viene assegnata a uno sviluppatore che aveva fatto una stima di qualche giorno allora quest’ultimo si troverà in difficoltà nel portare a termine il compito; per questo motivo è importante il contributo anche dei dev junior o inesperti.

Ci possono essere una serie di problemi di stima legati alla funzionalità in sé. Potremmo infatti avere stime:
- **molto differenti** (ore vs giorni): in questo caso, è possibile che la carta non sia descritta o compresa correttamente; se uno sviluppatore stima poche ore e un altro qualche giorno c’è qualche problema. In conclusione è necessario trovare un punto di incontro.
- **quasi uniformi, ma** **molto alte**: se la stima supera il tempo di iterazione potrebbe essere che la storia sia troppo **ampia**. Non si può neanche iniziarla in questo ciclo e continuarla nel prossimo: se alla fine dell’iterazione non ho portato a termine il lavoro prefissato è **come se non l’avessi fatto** (anche se era stato completato al 90%), perché il cliente non lo vede nella release e tale lavoro **non è dunque dimostrabile**. Per ovviare a questo problema si può fare lo **splitting delle carte**, ovvero scomporre una carta in più carte in modo da **dividere il problema in sotto-problemi.**
- **simili**: non bisogna prendere la più bassa, alta o la media. Si deve arrivare a un accordo in modo tale che chiunque nel team si riconosca nella stima effettuata.

Oltre a ciò, la fase di stima dei tempi si porta dietro diverse problematiche intrinseche, tra cui:
- **perdita di tempo**: per accordarsi su una stima comune si spende molto tempo (troppa comunicazione);
- **effetto àncora**: si tratta di un effetto che si verifica quando bisogna assegnare un valore ad una quantità ignota. Poiché il cervello umano è più bravo a ragionare per relazioni piuttosto che per assoluti, una volta che viene fatta la prima stima numerica questa definisce l’ordine di grandezza delle stime successive, facendo cioè da **punto di riferimento da cui è molto difficile distanziarsi**. Tale effetto impedisce di fare una stima che prenda obiettivamente in considerazione le sensazioni di tutti i membri del team, e va dunque assolutamente evitato.

Per evitare questi problemi e semplificare il processo di stima si sono sviluppati **diversi processi**, che data la loro **gamification** aumentano anche l’engagement degli sviluppatori in questa fase di pianificazione.

### Planning Poker
![Planning poker](https://marcobuster.github.io/sweng/assets/03_planning-poker.jpg)

Una per una vengono presentate brevemente le carte con le **user stories** facendo attenzione a non fare alcun riferimento alle tempistiche in modo da non creare subito un effetto ancora: in questa fase **il team può fare domande**, chiedere chiarimenti e discutere per chiarire assunzioni e rischi sulla user story, ma deve stare molto attento a **non fare alcuna stima**.

Poi ogni componente del team sceglie una carta dal suo mazzo personale per rappresentare la propria stima e la pone coperta sul tavolo: su queste carte si trovano una serie di numeri senza unità di misura che vanno da 0 a 100, seguendo un andamento non uniforme; il loro scopo è quello di definire un’**ordine di grandezza** piuttosto che una stima precisa. Ci sono anche delle carte particolari, ovvero:
- ❓ indica che non si è in grado di dare una stima;
- ☕ indica che la riunione è andata troppo per le lunghe e [serve una pausa](https://www.youtube.com/watch?v=-gAlDOcXgyM).

Fatta questa **prima stima blind** le carte vengono girate contemporaneamente: idealmente vi dovrebbe essere l’unanimità sulla stima. Se così non è chi ha espresso le stime più basse e più alte ha 1 minuto per **motivare la propria scelta** in modo da cercare di convincere gli altri; si noti che agli altri componenti del team non è concesso parlare per evitare di perdere troppo tempo!  
Finito questo momento di consultazione tutti i membri del team fanno una **nuova stima** e si continua così finché non si raggiunge l’unanimità. Solitamente le votazioni convergono dopo un paio di round.

**Ma qual è l’unità di misura** su cui si fanno le stime? **Dipende**: essa può essere scelta prima o dopo aver trovato un accordo e possono essere ore, giorni o pomodori (25 minuti senza alcuna distrazioni, e dopo c’è una pausa). Ovviamente non si può pretendere di lavorare delle ore senza alcuna distrazione, per cui in queste stime si considera anche un certo **slack time**, ovvero un tempo cuscinetto che comprende il **tempo perso** a causa di distrazioni.
### Team Estimation Game

Si tratta di un metodo un po' più complesso articolato in 3 fasi e basato sul confronto tra i diversi task piuttosto che sulla stima numerica. Esso si basa infatti sull’idea che sia semplice stabilire se un task sia più facile o più difficile di un altro, mentre è molto **più complicato capire di** **quanto** sia più facile/difficile. L’idea è dunque quella di suddividere in fasi il dare i valori ai task, considerandone sempre di più difficili per arrivare a fare una buona stima.

- ### Prima Fase: Valutazione comparativa
	![Prima fase del team estimation game](https://marcobuster.github.io/sweng/assets/03_team-estimation-1.jpg)
	Si fa una pila con le storie e si mette la **prima carta al centro del tavolo**. I dev si mettono in fila e uno alla volta eseguono queste azioni:
	- il **primo della fila estrae una carta dalla pila**, la legge ad alta voce e la **posiziona** a sinistra (più semplice), a destra (più complicata) o sotto (equivalente) la carta già presente sul tavolo.
	- il **prossimo dev** può:
	    - **estrarre una nuova carta dalla pila** e **posizionarla** secondo le stesse regole, eventualmente inserendola in mezzo a due colonne già presenti;
	    - **spostare una carta precedentemente posizionata**, commentando la motivazione della sua scelta. Può ovviamente succedere che tale carta venga rispostata nella sua posizione originale, ma dopo un po’ si troverà un accordo sulla difficoltà del relativo task.
	
	Terminata la pila avremo le carte disposte sul tavolo in **colonne di difficoltà comparabile**, ordinate dalla meno difficile (sinistra) alla più difficile (destra). Oltre ad aver ridotto la **comunicazione** (molte carte non saranno contestate), con questa tecnica abbiamo evitato anche l’**effetto ancora**, dato che l’assenza di valori precisi evita il rischio di influenzare eccessivamente gli altri. 
	Inoltre, a differenza del planning poker, **si può tornare sulle proprie decisioni**, cosa che favorisce un continuo adattamento e ripensamento delle stime.

- ### Seconda Fase: Quantificare distanze
	![Seconda fase del team estimation game](https://marcobuster.github.io/sweng/assets/03_team-estimation-2.jpg)
	Si cerca di quantificare le **distanze** tra le carte. 
	Ci si mette di nuovo in coda davanti al tavolo con il mazzo di carte del planning poker **(uno solo**, non uno per persona) e **si cerca di etichettare le colonne in base alle difficoltà**.
	
	Si posiziona la prima carta (solitamente si parte da 2 perché magari nella prossima iterazione può esserci qualcosa di ancora più facile) sopra la prima colonna.
	Quindi:
	- il **primo sviluppatore** prende il valore successivo e lo posiziona sulla prima colonna che pensa abbia quel valore (rispetto al 2), oppure lo posiziona tra due colonne se pensa che sia un valore di difficoltà intermedio tra le due.
	- lo **sviluppatore successivo** può invece:
	    - **estrarre una carta** dal mazzo e **posizionarla** secondo le regole di prima (la prima colonna che pensa abbia un particolare valore di difficoltà);
	    - **spostare una carta** con un valore precedentemente posizionato, commentando la motivazione dello spostamento;
	    - **passare** il turno, nel caso in cui non ci siano più carte nella pila e non si vogliono spostare altre carte.
	
	È possibile avere delle carte in cui sopra non c’è nessun numero, queste saranno assimilate alla colonna alla loro sinistra. 
	
	![](https://agilelearninglabs.com/wp-content/uploads/2012/05/team-estimation-game-with-fib-cards.jpg "team estimation game with fib cards")
	Esiste anche la possibilità di avere dei numeri senza alcuna carta sotto, questo significa che non esistono carte a cui è stato attribuito quel valore di difficoltà.
	
	![](https://agilelearninglabs.com/wp-content/uploads/2012/05/team-est-game-missing-21.jpg "team est game missing 21")

	Al termine di questa fase, la situazione sarà simile alla seguente:
	
	[![How to play the Team Estimation Game | Agile Learning Labs](https://agilelearninglabs.com/wp-content/uploads/2012/05/team-est-sorted-stories.jpg)
	![Fine seconda fase del team estimation game](https://marcobuster.github.io/sweng/assets/03_fine-seconda-fase-estimation-game.jpg)
- ### Terza Fase: Scala assoluta
	Si stima il tempo in ore/uomo di una delle carte più semplici e successivamente si calcolano tutte le colonne in proporzione alla prima.
	Ma questa fase è davvero cosi utile? Nella pratica si è visto che **è inutile valutare il lavoro fatto in ore/uomo**, anche perché con il passare del tempo può variare.
	La nozione di **velocity** risolve questo problema.

### Velocity

È importante riuscire a stimare la **velocità** con la quale stiamo avanzando. In fisica la velocità è data dal rapporto tra la distanza percorsa e il tempo per percorrerla. 
Questa proprietà può essere usata anche nella **gestione dello sviluppo agile**: il numeratore è il **punteggio delle storie** mentre il denominatore è la **lunghezza dell’iterazione** (assimilabile in un’unità di tempo).

La **velocity** nel mondo agile è quindi il **numero di story point** guadagnati nell’arco dell’**iterazione corrente**, proprio per questo motivo è poco oggettiva e molto variabile. Story point stimati in maniera non efficace (sovra o sottostimati) possono portare a pensare che un team sia molto veloce o lento quando effettivamente non è così. Si tratta infatti di un metro di valutazione **facilmente falsificabile**, che quindi non deve essere imposto, ma deve essere stimato e migliorato nel tempo per raggiungere un metro di paragone sempre più preciso.

Essa è la capacità (osservata) di completare lavori da parte del team, dunque riesce a dare un’idea di quanto si è riusciti a fare in termini di complessità astratta. Se per esempio il team è riuscito a fare 50 punti nella iterazione appena finita, è ragionevole prefissarsi di fare almeno 50 punti nell’iterazione successiva, ma non certo.

**La velocity** **non può essere usata** per dare **premi**, per **confrontare** team diversi o **punire** in caso di diminuzione, però si adatta al modo diverso dei dev di gestire le stime e al fatto che si tende a sottostimare o sovrastimare carte diverse.

Quando si aggiunge una persona questa metrica deve inizialmente restare invariata, per prevedere la sua formazione. Se la rimuovo ci sarà una perdita di produttività.

La velocity **non deve considerare le storie lasciate incompiute**. 
Inoltre, **non deve essere** **imposta**: la velocity di un team è fissa e non può essere aumentata, in quanto capacità osservata.

Esiste un movimento chiamato _**no estimates**_, che evita al team qualsiasi stima. Questa metodologia funziona in team molto maturi che sono in grado di guidare il cliente a formulare storie simili in termini di difficoltà, avendo tutti una misura standard per le storie.