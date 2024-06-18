È _meccanicamente_ possibile trasformare una **macchina a stati finiti** in una **rete di Petri**.

![[Da FSM a Rete.png]]

Riferendosi all’esempio del **produttore**, l’unico problema è l’**esistenza di collegamenti diretti tra posti**: come è stato detto in precedenza questo non è possibile in una **rete di Petri**. Sarà quindi necessario inserire tra i posti delle transizioni per avere una rete di Petri valida.

Immaginando di mettere un solo gettone in uno dei due posti della rete appena creata, questo indicherà lo **stato attivo** presente nella macchina a stati finiti.

Seguendo questi passaggi diventa banale mappare una macchina a stati finiti su una rete di Petri: di seguito vi è invece l'esempio di un consumatore e di un buffer.

![[Consumatore buffer.png]]

Componendo le reti di Petri di _produttore_, _consumatore_ e _buffer_ appena create, si crea la seguente.

![[Composizione reti.png]]

In termini di automi a stati finiti, per trovare gli **stati raggiungibili** da questa composizione sarebbe stato necessario eseguire il prodotto cartesiano tra gli stati delle tre macchine a stati finiti combinate tra loro. Trattandosi invece di una rete di Petri, è sufficiente unire tutti gli identificatori uguali in un unico identificatore (ad esempio la transizione deposita della rete _produttore_ e della rete _buffer_) e aggiungere a quest’ultimo tutti collegamenti posseduti dagli identificatori uniti.

![[Composizione reti 2.png]]

Precedentemente è stato detto che, _nel caso di una rappresentazione di una FSM in termini di una rete di Petri_, si rappresenta lo **stato attivo nella FSM** con un gettone: di conseguenza, portando all’interno della rete composta tutti i gettoni delle varie reti si arriva ad ottenere il risultato descritto dall’immagine seguente, in cui tutte le “entità” (_consumatore_, _produttore_ e _buffer_) mantengono la propria individualità (è infatti presente un gettone per ogni entità).
In questo caso si può quindi notare che * il produttore è pronto a produrre, il buffer è vuoto e il consumatore è pronto a consumare una volta che il buffer avrà al suo interno qualcosa*.

![[Composizione reti 3.png]]

### Come evolve questa rete?

Per rispondere a questa domanda la prima cosa è considerare quali sono le **transizioni abilitate**: in questo caso si tratta solo della transizione _produci_ sotto a $p_0$, in quanto è l’unica ad *avere tutti gli elementi del suo preset con un numero di gettoni sufficienti a farla scattare*; $p_0$ possiede infatti un gettone e l’arco ha peso 1 (_quando non è specificato il peso è 1_).  
**Una rete di Petri non forza lo scatto di alcuna transizione**, quindi volendo si potrebbe rimanere nello stato corrente *all’infinito* senza far mai scattare _produci_. Se però questa scatta, il gettone in $p_0$ viene distrutto e in $p_1$ viene generato un nuovo gettone.

![Primo scatto](https://marcobuster.github.io/sweng/assets/14_primo-scatto.png)

Dopo questo scatto la rete di Petri si trova in una situazione in cui **il produttore ha prodotto qualcosa** ed è pronto a **depositarlo nel buffer**: a questo punto non resta che porsi nuovamente la domanda _“quali transizioni sono abilitate?”_ per capire come può procedere l’evoluzione della rete.
Risulta facile notare come la transizione _deposita_ sotto $b_0$ sia l’unica abilitata e di conseguenza, _se dovesse scattare_, il risultato sarebbe il seguente:

![Secondo scatto](https://marcobuster.github.io/sweng/assets/14_secondo-scatto.png)

Ora è possibile identificare una situazione particolare, ovvero quella in cui **le transizioni pronte a scattare sono due**. Sorge spontanea la domanda: _“quale delle due transizioni scatta prima?”_. Nelle reti di Petri descritte fino ad ora non è stato presentato lo **scatto simultaneo** delle transizioni, ma nulla vieta che possa avvenire in un *contesto reale*, tipico nei sistemi concorrenti (dove non si ha questo tipo di controllo globale). In tal caso si tratterebbe di un’istanza di **non determinismo**, ovvero **non si può dire quale transizione deve scattare**. 
Sono quindi tre le situazioni che si possono verificare:
1. scatta la prima transizione;
2. scatta la seconda;
3. non scatta nessuna (la _non evoluzione_ è comunque un’**evoluzione**)

Nel caso in cui fosse stato necessario definire che una delle due transizioni scatti prima dell’altra, ci si troverebbe di fronte ad una rete **non corretta**: è infatti possibile modificare la rete in modo tale che imponga un ordine di scatto alle transizioni.


### Stiamo sfruttando le reti di Petri?

A questo punto è possibile chiedersi se si stiano sfruttando realmente tutte le **potenzialità delle reti di Petri**. La risposta è: non molto, siccome la rete dell’esempio precedente è stata ricavata mediante una traduzione "automatica" dagli **automi a stati finiti**. Per capire meglio ciò è possibile osservare un secondo esempio in cui è presentata una rete alternativa alla precedente, ma con lo stesso scopo.

![[Sfruttamento reti.png]]

La differenza che salta subito all’occhio è il numero di gettoni presenti all’interno di $B_0$ ($B_1$) che indicano il numero di posizioni libere (posizioni piene per $B_1$) nel buffer. Questo è un **vantaggio** perché se il buffer dovesse **cambiare la sua capienza**, sfruttando questa rete è sufficiente modificare la marcatura di $B_0$ e il problema sarebbe risolto; la **rete precedente** avrebbe invece bisogno di una **pesante modifica per essere adattata**.  
Di conseguenza si può applicare lo stesso concetto per il **consumatore** e per il **produttore**: aumentandone il numero dei gettoni (rispettivamente in $P_0$ e $C_0$) aumenterebbe il numero di entità in grado di produrre e consumare.

![Rete alternativa diverse entità](https://marcobuster.github.io/sweng/assets/14_rete-alternativa-diverse-entita.png)

Si può quindi affermare che cambiando il **numero di gettoni** è possibile **moltiplicare gli elementi del sistema** di cui si vuole tracciare l’**evoluzione**. Si sottolinea ancora che questo, se fosse stato riadattato in una **FSM**, **risulterebbe molto oneroso** in termini di dimensioni.

#### A volte "less is better"

Per definizione le **FSM** **non possono rappresentare situazioni infinite**, se si volesse quindi modificare ancora l'esempio sopra imponendo una capienza illimitata al buffer, non sarebbe possibile usando una FSM.
Sfruttando le **reti di Petri** invece è sufficiente eliminare l'identificatore del posto $B_0$: in questo modo si ha una situazione in cui i *produttori* possono depositare senza limiti all'interno del *buffer*, mentre i *consumatori* non possono prelevare più elementi di quelli presenti nel buffer. Questo vincolo è imposto dalla marcatura di $B_1$, infatti la transizione *preleva* può scattare al massimo $n$ volte consecutivamente, dove $n$ è la marcatura di $B_1$ (assumendo che nel mentre non avvengano depositi da parte dei produttori).

![[Sfruttamento posto in meno.png]]

#### Altre modifiche

Un'altra modifica applicabile all’esempio sfrutta i **pesi degli archi**: ponendo un peso di $3$ all’arco che collega _deposita_ a $B_1$ si può dire che il *produttore* crea e deposita tre prodotti, occupando tre posizioni nel buffer. Ponendo invece un peso di $2$ all’arco che collega $B_1$ a _preleva_ si specifica che è possibile prelevare dal buffer due elementi alla volta. Questo esempio, in parte forzato, è utile per chiarire il fatto che **nelle reti di Petri agli archi è possibile attribuire un significato**, non sono semplici collegamenti.

Vengono infatti informalmente chiamati **archi**, rifacendosi alla terminologia dei *grafi*, ma in realtà indicano una **relazione più profonda** che coinvolge due identificatori: in questo esempio esiste infatti una relazione per cui ogni elemento prodotto occupa tre posizioni all’interno del buffer e un’altra relazione in cui ogni consumatore può prelevare obbligatoriamente due elementi alla volta. 
Tramite il peso degli archi è possibile creare delle **situazioni ambigue**: ad esempio se la relazione che coinvolge _deposita_ e $P_0$ avesse un peso di $2$, ogni volta che viene prodotto qualcosa i produttori si moltiplicherebbero e ovviamente questa situazione indicherebbe che la rete è sbagliata, quindi è necessario fare attenzione ad evitare questo tipo di situazioni.

![Archi con pesi](https://marcobuster.github.io/sweng/assets/14_archi-con-pesi.png)

Si sottolinea che **è possibile ridurre una rete P/T avente pesi sugli archi in una [[Eliminazione pesi sugli archi|rete P/T senza pesi sugli archi]]**.