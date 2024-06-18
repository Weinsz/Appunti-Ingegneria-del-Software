
**Verifica e convalida** sono due termini con un significato apparentemente simile ma che celano in realtà una differenza non banale tra loro:
- **convalida** (*dell'[[Qualità del software#^b2d6a2|affidabilità]]*): si intende l'attività di confronto del sw con i **requisiti** posti dal cliente/committente, che sono **informali**.
- **verifica** (*della [[Qualità del software#^f0fad0|correttezza]]*): si intende l'attività di confronto del sw con le **specifiche** prodotte dall'analista, che sono **formali**;

Ci sono quindi due punti critici che vanno a evidenziare maggiormente questa differenza:
1. **requisiti e specifiche sono spesso formulati diversamente**. Solitamente i **requisiti**, venendo scritti dal **cliente**/committente, sono formulati in un linguaggio più vicino al suo dominio. D'altro canto, le **specifiche** sono scritte in un linguaggio più vicino al dominio dello **sviluppatore**, spesso in modo formale e con poche ambiguità.
2. **è facile che i requisiti cambino in corso d'opera, mentre le specifiche restano congelate**: quest'aspetto dipende molto dai **contratti** tra committente e team di dev.

La definizione dei **requisiti** forniti dal cliente è **immediata ma informale**: scrivere dei test che li **convalidano** può risultare **complicato**. Invece, è **più semplice** validare le **specifiche** attraverso test in quanto sono scritte dal team di sviluppo e sono dunque **più formali** e complete.

Richiamo a [[Modello a V]] con verifica e convalida come frecce.

Si vedrà:
- [[Terminologia ed Errori]]
- [[Verifica e Convalida/Tecniche|Tecniche]]