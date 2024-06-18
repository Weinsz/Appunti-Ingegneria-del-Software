Ora ci si può chiedere se sia possibile creare una *struttura dati* (**albero** e **grafo**) anche per le **[[Limitatezza|reti illimitate]]**, i cui nodi rappresenteranno **gruppi di stati *potenzialmente infiniti***.

Si introduce innanzitutto il concetto di **copertura/copribilità**:
Una marcatura $M$ **copre** una marcatura $M'$ se e solo se: $$ \forall p \in P \quad M(p) \ge M'(p) $$
I posti per cui $M(p) > M'(p)$ si dice che sono coperti in maniera **propria**.
Al contrario, $M$ è detta **copribile** da $M'$ se e solo se: $$ \exists M'' \in R(P/T, M') \text{ che copre M}$$
Grazie al concetto di **copertura** è possibile ridefinire quello di **transizione morta**:
![[Transizione morta.png]]
La **marcatura minima** $M$ per abilitare $t$ è definita come: $$ \forall p \in \text{pre}(t) \quad M(p) = W(\langle p, t \rangle) \space e \space \forall p \in P \setminus \text{pre}(t) \quad M(p) =0 $$
La transizione $t$ è **morta** sse $M$ non è copribile da nessuna marcatura a partire dalla marcatura corrente $M'$, vale a dire: $$  \nexists M'' \in R(P/T, M') \text{ che copre M} $$, cioè per cui: $$ \forall M'' \in R(P/T, M') \quad \forall p \in P \quad M''(p) < M(p)$$
In caso contrario la transizione $t$ è almeno 1-viva.

Si conclude quindi che se una marcatura ne copre un’altra, tutte le azioni possibili nella seconda **sono possibili** anche nella prima. È quindi possibile modificare l’**albero di raggiungibilità** in modo tale che, quando viene creato un nodo, è necessario verificare se tra i suoi predecessori ne esiste uno che lo copre, allora a questo punto nei posti dove c’è copertura propria (ovvero $M(p) > M′(p)$) si mette ω.

Il **simbolo** $\omega$ rappresenta un numero **grande a piacere** (e non *qualsiasi*), che può aumentare all'infinito: quest'aspetto è da tenere in considerazione *quando bisogna cercare quali transizioni sono abilitate da esso*. Questo tipo di notazione ($\omega$) viene introdotta per **limitare l’aumento spropositato di nodi** nel diagramma, comprimendo marcature uguali se non per ω.

Se una marcatura $M$ copre una precedente $M'$, infatti, è possibile **ripetere gli scatti** delle transizioni in $M'$ per arrivare ad $M$; se al termine di quest'operazione sono presenti più gettoni in un posto, allora è possibile crearne un numero grande a piacere.

Risulta importante notare come le transizioni che erano **abilitate** in una certa marcatura $M'$ lo saranno anche in una marcatura diversa che copre $M'$ (in quanto se era possibile in quella con gettoni minori, lo sarà ovviamente anche in quella con più gettoni), a meno che non ci siano **[[Archi inibitori]]**.

Si può ora definire l’**algoritmo** per la creazione di un **albero di copertura**, comunque simile in molti punti al precedente:

01    **crea la radice** corrispondente alla marcatura iniziale $M_0$, etichetta il nodo come **nuovo**; 
02    **==finché== esistono nodi etichettati come "nuovo"** esegui:
03        **seleziona** una marcatura $M$ con etichetta **"nuovo"** e **rimuovi l'etichetta**.
04        **==se==** la **$M$ è identica** a una marcatura sul cammino dalla radice a $M$ allora:
05            **etichetta** $M$ come **"duplicata"**;
06            **==continua==** alla prossima iterazione.
07        **==se==** **nessuna transizione** è **abilitata** in $M$ allora:
08            **etichetta** la marcatura come **"finale"**;
09
10        **==finché== esistono transizioni abilitate in $M$** esegui per ognuna di esse:
11            **crea la marcatura $M'$** prodotta dallo **scatto di $t$** (cioè *fai scattare $t$*);
12            **==se==** sul cammino **dalla radice $M_0$ a $M$ esiste una marcatura $M''$ coperta da $M'$**, allora:
13                **modifica** $M'$ scrivendo $\omega$ **in tutte le posizioni corrispondenti a ==coperture proprie==**.
14            **crea un nuovo nodo** corrispondente a $M'$;
15            **aggiungi un arco** nell'albero da $M$ a $M'$;
16            **etichetta la marcatura $M'$** come **"nuovo"**.

Dall’albero generato da questo algoritmo è possibile arrivare al **grafo di copertura**.
Inoltre, ripetendo l’algoritmo precedente su una **rete [[Limitatezza|limitata]]** viene generato un grafo di copertura senza $\omega$ e quindi equivalente a un [[Albero di raggiungibilità]].


> [!NOTE] Termina sempre
> L’algoritmo **termina in ogni caso**: è sufficiente **osservare** l’albero risultante per stabilire se la rete considerata è limitata oppure no.


### Esempio

Partendo dalla rete di Petri sottostante ed applicando l’**algoritmo** appena descritto è possibile arrivare ad un **albero di copertura**.

![[Rete albero copertura.png]]

Come visto nell’**esempio della creazione di un albero di raggiungibilità**, il primo passo da fare è **creare il nodo radice** corrispondente alla marcatura iniziale (`100`) e marcarlo come nuovo. 
Successivamente, è necessario considerare l’unico nodo esistente (`100`) e iterare tra le sue transizioni. In questo caso, è abilitata la transizione $t_0$ che porta a una marcatura $M'=$ `101`.


A questo punto si può notare come la radice sia una **marcatura coperta da M′**, in quanto:
- $M'\space|1≥1|\space M$;
- $M'\space|0≥0|\space M$;
- $M'\space|1 > 0|\space M$.

Nel nodo corrispondente alla marcatura $M'$ è quindi possibile **sostituire l’unica copertura propria** (quella con il $>$ e non il $≥$) **con il simbolo ω** e marcare il nodo come **"nuovo"**.
Questa è l’**unica parte dell’algoritmo differente** da quello che genera l’albero di raggiungibilità: il resto dell’esempio è quindi completato dall’immagine sottostante.

![](https://marcobuster.github.io/sweng/assets/15_esempio-albero-copertura-albero.png)

Tramite lo stesso procedimento attuato per gli alberi di raggiungibilità, è possibile trasformare il precedente albero in un **grafo di copertura**:

![](https://marcobuster.github.io/sweng/assets/15_esempio-albero-copertura-grafo.png)


### Considerazioni

- se $\omega$ non compare mai nell’albero di copertura la rete è **limitata**;
- una rete di Petri è **binaria** se nell’albero di copertura compaiono solo 0 e 1;
- una transizione è **morta** (0-viva) **se non compare mai come etichetta di un arco dell’albero di copertura**;
- condizione necessaria affinché una marcatura M sia **raggiungibile** è l’esistenza di un nodo etichettato con una marcatura che copre M (non sufficiente: _le marcature coperte non sono necessariamente raggiungibili_). Es. marcatura: `010` è coperta da `011`, con nodo `01ω`.
- non è possibile stabilire se una rete è **viva**, perché non so stabilire la marcatura precisa in cui finisco, ma si indica solo un gruppo di stati possibili; in più, non si sa se ogni transizione può scattare infinite volte. 

### Esempio

È doveroso un ulteriore esempio particolare nel caso di reti **non vive**.  
Data una _rete non viva_ (come nella figura sotto) dall’albero di copertura **non è possibile** evincere se la rete è effettivamente viva o no: infatti se il nodo `01ω `è duplicato esso non verrà più espanso. 
A questo punto non è possibile aggiungere all’interno dell’albero il nodo `010`, in cui la rete raggiunge un deadlock (**considerando l'arco rosso**), motivo per il quale è **non viva**. Questo però significa che quest'albero di copertura è uguale a quello della stessa rete **senza arco** che collega $p_3$ a $t_4$, che in quel caso è una **rete viva**. Detto ciò si può affermare che tramite l’albero di copertura non è possibile dire se una rete è viva oppure no.

![](https://marcobuster.github.io/sweng/assets/15_esempio-particolare.png)

![[Rete albero copertura 2.png]]
#### Da albero di copertura a rete

Passare dall’albero di copertura alla rete di Petri è un’operazione che rispetto all’inverso crea più **incertezza**. **L’albero di copertura permette infatti di rappresentare reti potenzialmente illimitate**, è quindi normale avere come risultato reti di cui non si conosce la struttura: molte reti potrebbero essere associate **allo stesso albero**.

Nel seguente esempio si può notare come la rete ricavata presenta degli _archi tratteggiati_: **potrebbero essere presenti**, oppure no. Inoltre, sono assenti anche i pesi negli archi. Tale mancanza di informazioni è dovuta in gran parte dalla presenza di ω: un nodo con all’interno ω rappresenta **diverse marcature**.

![](https://marcobuster.github.io/sweng/assets/15_esempio-da-albero-a-rete.png)

È importante notare come le marcature **sicuramente raggiungibili** siano quelle i cui nodi nell’albero di copertura non contengono ω: *delle altre non v'è certezza.*