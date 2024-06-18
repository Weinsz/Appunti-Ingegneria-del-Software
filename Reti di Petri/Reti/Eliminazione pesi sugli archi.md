Si è detto che per ogni rete avente dei pesi sugli archi è possibile crearne una **equivalente senza pesi** sugli archi (ovvero avente tutti gli archi di peso 1).  
Per fare ciò è necessario considerare due casi distinti:
- con peso sugli archi in **ingresso** ad una transizione;
- con peso sugli archi **in uscita** da una transizione.

### In ingresso in un posto (uscita da una transizione)

In questo caso il peso da rimuovere è su un arco che esce da una transizione ed entra in un posto.
Per poter fare questa modifica è necessario avere lo **scatto di una nuova transizione** (in quanto non è possibile collegare due archi dallo stesso posto alla stessa transizione), ma non basta. 

![[Eliminazione pesi.png]]

Dopo lo scatto di $t_0$ è possibile che $T_0^{bis}$ non scatti e la rete evolva senza che in $p_1$ ci sia il giusto numero di gettoni (problema di concorrenza).

Per risolvere questo problema si sfrutta una sorta di **lock**, ovvero un posto collegato **bidirezionalmente** con tutte le transizioni della rete tranne per $t_0$, a cui è collegato solo in ingresso, e per $T_0^{bis}$, a cui è collegato solo in uscita. In questo modo è come se lo scatto di $t_0$ sia scomposto logicamente in due parti: quando $t_0$ scatta viene attivato il lock in modo tale che nessun’altra transizione sia abilitata e, successivamente, lo scatto di $T_0^{bis}$ lo rilascia. 
Questo ovviamente non obbliga $T_0^{bis}$ a scattare immediatamente, però è certo che la rete non potrà evolvere in alcun altro modo e quindi non si creeranno marcature non esistenti nella rete originale. Questa soluzione non è molto elegante perché esiste un posto avente in ingresso un arco per ogni transizione della rete.
### In uscita da un posto (ingresso in una transizione)

In questo caso il peso da rimuovere è su un arco che esce da un posto ed entra in una transizione, dunque è necessario che vengano **distrutti due gettoni** dallo stesso scatto.

![Eliminazione pesi archi uscita](https://marcobuster.github.io/sweng/assets/14_eliminazione-archi-uscita.png)

L’approccio da utilizzare è **simile**: è infatti presente un **posto globale** che fa da **lock** in modo da risolvere il problema di concorrenza tra $t_8$ e $t_1$. In questo caso però è presente un ulteriore problema, ovvero al momento dello scatto di $t_8$ il gettone in $p_0$ viene consumato, di conseguenza $t_1$ non può scattare. Inoltre il resto della rete rimane bloccata, in quanto all’interno del posto globale non è più presente il gettone che è stato consumato sempre dallo scatto di $t_8$.  
Questo **deadlock** può essere risolto aggiungendo un controllo sul posto $p_0$, in modo tale che possa scattare solo quando possiede due o più gettoni: in questo modo non può verificarsi la situazione in cui $t_8$ scatti senza un successivo scatto di $t_1$.

Il meccanismo della rete inizia ad essere **molto complesso**: nell’esempio viene mostrato solo il caso in cui devono essere consumati **due gettoni**. In altri casi con più gettoni, o con situazioni differenti, la rete aumenterebbe ulteriormente di complessità. Risulta quindi più facile pensare la rete in modo differente.

La tecnica descritta non è infatti l’unica esistente per modellare il sistema: nonostante possa essere adatta per questo particolare esempio, è comunque possibile trovarne un’altra per modellare una rete senza sfruttare i pesi o una loro **traduzione meccanica**.

### Reti Condizioni - Eventi

Le reti $C/E$ (condizioni - eventi) sono delle particolari **reti più semplici**, in cui:
- tutti gli **archi** hanno peso 1;
- tutti i **posti** hanno capacità massima 1;

A prima vista possono sembrare poco modellabili, ma è in realtà è un tipo di rete più semplice e immediata da capire. 
Infatti: 
- i **posti** corrispondono alle **condizioni** (vere o false a seconda della presenza del gettone), come una variabile *booleana*;
- le **transizioni** corrispondono agli **eventi** (che scattano quando un insieme di condizioni risulta vero).


> [!NOTE] [[Limitatezza]] e $C/E$
> Ogni rete $P/T$ **limitata** è **traducibile** in un'equivalente **rete $C/E$**. 

Per le **reti illimitate** invece **non si può** trovare una traduzione poiché non si possono rappresentare infiniti stati con un tipo di rete che per definizione è limitata.