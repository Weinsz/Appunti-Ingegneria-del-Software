Ulteriore evoluzione dello [[State diagram]], il **Superstate** consente di rappresentare più facilmente una **gerarchia di stati**.

Esempio classico: il diagramma sottostante rappresenta il funzionamento di un semaforo. 
Questo schema però presenta alcuni difetti, tra cui:
- **Ridondanza**: da ogni stato è possibile passare allo stato `spegni`, e questo viene rappresentato con una freccia per ogni stato;
- **Disomogeneità**: a livello concettuale, dire che un semaforo è verde quando non è spento ha poco senso, dovrebbe essere acceso, questo rende meno intuitivo e più confusionario il diagramma.

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/caaeb02245513f0dc37168ebea1b625b6987c4c2.svg)]

Per ovviare a questo problema è possibile descrivere uno stato tramite un altro diagramma UML degli stati, ovvero partendo da uno stato è possibile avere una transizione che conduce a un’altra FSM concettualmente *innestata*.

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/02888cd056e834c0bf9c81b30f40e289ec6d214d.svg)]

Si potrebbe pensare però che ogni semaforo al momento dell’accensione sia verde, ma questo non è corretto, soprattutto se si pensa a un incrocio. È quindi possibile associare al diagramma uno stato **_history_**, il cui scopo è memorizzare lo stato storico prima dell’interruzione dell’FSM, in modo da riprendere il funzionamento da dove si era interrotto.

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/b19b95b3f85c76167520a40d728ae5ed4db1f4dc.svg)](https://marcobuster.github.io/sweng/mdbook-plantuml-img/b19b95b3f85c76167520a40d728ae5ed4db1f4dc.svg)

Si può far sì che il diagramma sia in grado di rappresentare il concetto di **concorrenza** tramite la divisione in **regioni** (ognuna regolata da una propria FSM). Esse possono essere attive contemporaneamente. I confini tra regioni, come mostrato nell’esempio, sono identificati da linee tratteggiate.

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/8e97c48ae2135e92973cfb181b47acfaf3b7470f.svg)]