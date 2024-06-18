![Modelli trasformazionali](https://marcobuster.github.io/sweng/assets/02_transformational-models.png)

Diametralmente opposti all'incubo del [[Pinball Life-Cycle]] si trovano i **modelli trasformazionali**, che pretendono di controllare ogni passo e procedimento in **modo formale** e di massimizzare il numero di incrementi.

Partendo dai requisiti informali, essi procedono tramite una sequenza di **passi di trasformazione** dimostrabili formalmente fino ad arrivare alla versione finale. Si basano sull'idea che, se le specifiche sono corrette e i passi di trasformazioni dimostrati, allora ottengo un programma corretto, cioè aderente alle specifiche.
Inoltre, la presenza di una **storia delle trasformazioni** applicate permette un rudimentale **versioning**, con la possibilità di tornare indietro a uno stato precedente del progetto, annullando le trasformazione fatte.

![Trasformazioni formali](https://marcobuster.github.io/sweng/assets/02_formal-transformations.jpg)

Ad ogni passo si ottiene un **prototipo** che differisce dal prodotto finale per efficienza e completezza, ma che è possibile trasformare ed ottimizzare in un altro migliore. Non è un processo del tutto automatico, anzi, ad ogni passo di trasformazione è richiesto un intervento umano che scelga cosa ottimizzare.

Si introduce il concetto di **prova formale di correttezza** delle trasformazioni applicate. A causa di quest'approccio rigido, sono applicati solo in ambienti di ricerca o progetti sia hw sia sw, come sviluppo di CPU.