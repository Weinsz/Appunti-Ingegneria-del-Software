Numerosi studi hanno provato a confrontare l’efficacia di varie tecniche di [[Utilità di un test|testing]], con particolare riferimento a testing **strutturale**, testing **funzionale** e [[Verifica e Convalida/Processi di review/Software inspection/Software inspection|Software inspection]]. Un [articolo](https://web.archive.org/web/20060920113729/http:/www2.umassd.edu/SWPI/ISERN/ISERN-98-10.pdf) del 2004 riporta in una **tabella di confronto** i risultati di alcuni di questi studi, considerando come **metrica** di valutazione delle tecniche di [[Verifica e convalida]] la _**percentuale media di difetti individuati**_.

![Confronto tecniche verifica e convalida](https://marcobuster.github.io/sweng/assets/13_tabella-confronto-tecniche-vc.png)

Come si può notare, a seconda dello studio appare più efficace l’una o l’altra tecnica; inoltre, la **somma delle percentuali per ogni riga** non è 100%, il che significa che alcuni difetti non possono essere rilevati da nessuna delle tre tecniche.
Nonostante ciò, si possono fare una serie di osservazioni: innanzitutto, l’efficacia di una o dell’altra tecnica dipende dalla **tipologia del progetto** su cui viene esercitata. Inoltre, **non è detto** che tecniche diverse trovino gli **stessi errori**: l’*ispezione* potrebbe aver trovato una certa tipologia di errore mentre il testing funzionale un’altra; le diverse tecniche controllano infatti diversamente **aspetti differenti** del programma, osservandolo da **diversi punti di vista**.

Confrontare le varie tecniche non è dunque necessariamente una perdita di tempo, mentre lo è sicuramente **confrontare solo i numeri**, come la varietà di risultati diversi ottenuti da parte di studi diversi. In più, dal riassunto della tabella si **perdono** informazioni sulle **modalità di rilevazione** dei dati, attribuendole ad **espressioni generiche** (come _comunemente_, _in media_, _progetti junior_…).

> Non c’è una risposta semplice al confronto e **non esiste una tecnica _sempre_ migliore** rispetto alle altre.


### Combinare le tecniche

Viene da chiedersi: 
#### Cosa può succedere se si **combinano insieme** diverse tecniche di verifica e convalida?

Diversi [studi](https://web.archive.org/web/20070221162909/http://www2.umassd.edu/SWPI/TechnicalReview/r4094.pdf) mostrano che applicando tutte e quattro le tecniche qui descritte — anche se solo in modo superficiale — il risultato è sicuramente **più performante delle tecniche applicate singolarmente**.

![Tabella tecniche verifica convalida insieme](https://marcobuster.github.io/sweng/assets/13_tabella-tecniche-vc-insieme.png)

Anche se una **certa percentuale di errori** può essere rilevata senza alcuna **tecnica formale di verifica e convalida**, semplicemente usando il software, si può infatti notare che:
- ciascuna tecnica presa singolarmente migliora tale percentuale iniziale,
- e soprattutto, la **combinazione** di tecniche diverse la incrementa ulteriormente. 
Questo perché tendenzialmente **ogni tecnica controlla aspetti differenti** e le rispettive **aree di controllo** si **sovrappongono poco**.

> Dunque è conveniente applicare superficialmente **ciascuna tecnica** rispetto a una sola tecnica in modo molto approfondito.

In conclusione, come afferma la **Legge di Hetzel-Meyer (L20)**:
> Una combinazione di diversi metodi di [[Verifica e convalida]] supera qualsiasi metodo singolo.