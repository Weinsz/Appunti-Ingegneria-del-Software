Consolidato su due fronti:
1. i clienti scrivono **test di accettazione** (o funzionali) sulle schede per aumentare la loro fiducia nel programma
2. i dev scrivono i **test di unità** perché la fiducia nel codice diventi parte del programma stesso

Nell'[[eXtreme Programming (XP)]] ogni aspetto viene massimizzato, ma in particolare il **testing** viene esasperato di più in quanto, oltre ad essere molto importante, molti altri aspetti si basano su di esso. Ha il ruolo di **rete di protezione** in tutte le fasi: ogni cambiamento è verificabile tramite i test.

Il testing aiuta molto anche quando non si parte da zero col programma, anche in modalità non agile. Prima di apportare modifiche al codice scrivo i test e solo successivamente procedo, in modo da non causare problemi. In più, solitamente non si fanno test su cose non modificate.

Il testing spesso viene lasciato alla fine, dopo lo sviluppo del progetto, ma facendo così è facile trascurare la fase di testing non identificando possibili errori.
Infine il testing facilita la fase di [[Prodotto e Processo/eXtreme Programming/Tecniche/Refactoring|Refactoring]], perché se il test non fallisce anche dopo aver modificato il codice della feature abbiamo la sicurezza di non averla alterata.

Un altro concetto importante è che i test dovrebbero **coprire tutte le righe di codice**, infatti non possiamo provare la correttezza del codice se non testandolo in ogni sua possibile forma ed esecuzione.