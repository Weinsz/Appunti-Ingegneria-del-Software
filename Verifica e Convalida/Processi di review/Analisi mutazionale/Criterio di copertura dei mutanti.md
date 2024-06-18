Un test $T$ soddisfa il **criterio di copertura dei mutanti** se e solo se per ogni mutante $\pi \in \Pi$ esiste almeno un caso di test $t \in T$ la cui esecuzione produca per il mutante $\pi$ un risultato diverso da quello prodotto da $P$.

**Metrica**: **frazione di mutanti $\pi$ riconosciuta come diversa da P** sul totale di mutanti generati. Se non vengono scovati tutti i mutanti sarà necessario **aggiungere dei casi di test** che li riconoscano. ^eb3f8d

I **tre passi** da seguire per **costruire un test con l'analisi mutazionale** sono dunque:
1. **analisi** delle classi e [[Generazione dei mutanti]];
2. **selezionare** dei casi di test da aggiungere a $T$, in base alla metrica appena descritta;
3. **esecuzione** dei casi di test sui mutanti, con un occhio alle performance.

Nell'[[Automazione dell'analisi mutazionale]] verranno viste più in dettaglio.