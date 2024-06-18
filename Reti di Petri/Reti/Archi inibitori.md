Esiste un'altra estensione delle **reti di Petri** in cui si utilizzano gli **archi inibitori**, ovvero archi che indicano la situazione in cui una transizione ha bisogno che **non siano presenti gettoni nel posto** affinché la transizione sia abilitata. 
Un **arco inibitore** di peso $n$ indica che la transizione collegata è abilitata se nel posto collegato sono presenti **meno di $n$ gettoni**.

![[Archi inibitori.png]]

In caso di **rete limitata** la **potenza espressiva** di una rete che sfrutta gli archi inibitori **non cambia**, perché esistendo un limite massimo $k$ di gettoni all’interno della rete sarà sufficiente creare un **posto complementare** contenente un numero di gettoni tali per cui la somma tra quest’ultimi e i gettoni presenti nel posto considerato sia minore o uguale di $k$. 

A questo punto è necessario che siano presenti due archi (uno in ingresso e uno in uscita) di peso $k$, in modo da permettere lo scatto della transizione solo nel caso in cui tutti i gettoni siano all’interno del posto complementare.
In realtà **non è necessario** che tutta la rete sia limitata, **è sufficiente che il singolo posto lo sia**: è necessario garantire che qualunque sia lo _stato generale_ della rete, in **quel preciso posto** non ci siano più di $k$ gettoni.

Nel caso di una rete **non limitata** (senza nemmeno il singolo posto limitato) invece non è sempre possibile avere una **traduzione equivalente** della rete di Petri: la **potenza espressiva** delle reti con gli archi inibitori **aumenta**.

> [!NOTE] Perché non piacciono al prof?
> Il **problema degli archi inibitori per il prof** è che rendono **inutilizzabili** alcune **tecniche di [[Analisi delle reti di Petri|analisi]]** che verranno affrontate successivamente.