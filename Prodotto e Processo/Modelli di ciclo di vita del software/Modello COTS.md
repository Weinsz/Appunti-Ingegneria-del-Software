COTS: Component Off The Shelf.

Si concentra sulla **riusabilità**, partendo dalla disponibilità interna o sul mercato dei moduli pre-esistenti sui quali basare il sistema, dovendo quindi solo integrarli tra loro.
Non è un approccio facile, necessita di dialogo tra componenti non per forza già pronte a comunicare come desidero.
![Modello COTS](https://marcobuster.github.io/sweng/assets/02_cots.png)

Si tratta però di un modello diverso perché richiede attività diverse:
- Analisi dei requisiti
- Analisi dei componenti: prima di progettare valuto la disponibilità di componenti che implementano una parte o tutte le funzionalità richieste
- Modifica dei requisiti: stabilisco se il cliente è disposto ad accettare un cambiamento nei requisiti necessario per utilizzare un certo componente
- Progettazione del sistema con riuso dei componenti: occorre progettare il sistema per far interagire componenti che non necessariamente sono stati progettati per farlo
- Sviluppo e integrazione
- Verifica del sistema

I lati positivi di questo approccio risiedono nel fatto che non si debba sviluppare tutto da zero ma vengono utilizzate delle componenti pre-esistenti. D’altro canto, qualora il numero di componenti sia troppo elevato, il lavoro di adattamento sarà molto complesso, e le funzionalità non necessarie di quest’ultime andranno a inficiare sul risultato finale del progetto, diminuendone ad esempio l’efficienza.