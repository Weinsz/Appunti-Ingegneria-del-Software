Dal [[Modello a cascata]] nascono poi numerose varianti che provano a risolvere i vari problemi.
Spicca per rilevanza il **Modello a V**, detto anche a **denti di pesce cane**, che introduce fondamentalmente una **più estesa fase di testing**.

![Modello a V](https://marcobuster.github.io/sweng/assets/02_v-model.png)

Sebbene sia ancora un [[Modelli sequenziali|modello sequenziale]] come quello a cascata, vengono infatti evidenziati **nuovi legami** tra le fasi di sviluppo, che corrispondono alle attività di [[Verifica e convalida|verifica e convalida]]: alla fine di ogni fase si *verifica* che il semilavorato ottenuto sia conforme alla **specifica** espressa dalla fase precedente, e inoltre si richiede la *convalida* del fatto che il semilavorato sia in linea coi veri vincoli e necessità del **cliente**.
Dunque, questo modello si concentra sul rapporto col cliente, continuamente coinvolto con la richiesta di **feedback** su ciascun sottoprodotto generato. Inoltre, ogni fase include delle **frecce implicite** dirette verso sé stessa, indicando la necessità di una verifica per garantire la coerenza e la logica del risultato prodotto.

Le due nuove attività introdotte sono dunque:
- **verifica** (frecce bianche): controlla la correttezza rispetto alla descrizione formale delle specifiche. In queste verifiche non è coinvolto il cliente;
- **validazione** (frecce grigie): controlla la compatibilità del sistema con le esigenze del cliente tramite un feedback continuo.