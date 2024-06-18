Volendo ricevere feedback rapidi dal cliente è necessario **integrare spesso**, anche **più volte al giorno**. Ciò non significa far passare i test d'unità per integrare tutto in un'unica operazione, ma essere **graduali**: è frequente scoprire che parti testate e funzionanti singolarmente, una volta integrate nel prodotto finale, non funzionano.

Si tratta di una tecnica di [[eXtreme Programming (XP)]] largamente usata in tutti i campi, non solo nello sviluppo sw. Se effettuata spesso dovrebbe risultare in un'azione semplice e veloce date le poche modifiche dalla versione precedente.

Al termine dello sviluppo di una **feature**, è compito della [[Pair programming|coppia]] integrarla nella **macchina di riferimento**, il cui accesso va regolato in maniera **esclusiva**: in situazioni di lavoro da remoto si può utilizzare un token. La macchina si trova in una situazione **monotona crescente**, per ciò che riguarda le funzionalità. 

Ad ogni integrazione è necessario produrre qualcosa di consegnabile al cliente.
Una **user story** si dice **completata** solo dopo aver finito l'integrazione, superato test d'integrazione e aver mostrato al cliente il risultato della macchina di riferimento dopo l'integrazione.

Un altro vantaggio della continua integrazione è che evita la situazione in cui una coppia modifichi la macchina **dopo molto tempo** dalla propria ultima integrazione. Facendo così invece aumenterebbe in modo significativo la probabilità di errore per le altre coppie.

**Se una coppia non riesce a integrare blocca anche le altre**, che non possono andare avanti con le user story. Quindi sarà necessario che quella coppia rinunci, ritorni sulla propria macchina e cerchi di risolvere lì, testando il tutto prima di farlo su quella comune di riferimento.

