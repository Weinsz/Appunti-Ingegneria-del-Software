![Modello a fontana](https://marcobuster.github.io/sweng/assets/02_fountain-model.png)

Amplia il concetto di iterazione permettendo in qualunque momento di **tornare alla fase iniziale**.

Se ci si accorge di errori si torna all'inizio (**software pool**) e vengono **ricontrollate tutte le fasi** **precedenti**. Ovviamente ciò non implica l'eliminazione di tutto il lavoro fatto, quanto piuttosto risolvere l'errore con un approccio che parta dalla modifica dei requisiti (se possibile), delle specifiche e **solo dopo del codice**, evitando di mettere una toppa solo a questo alla buona, come nel modello *code-and-fix*.
Una volta risolto il problema dalle fondamenta/alla radice si può **risalire velocemente** attraverso le altre fasi, mantenendo il lavoro già svolto e in più controllando che non si siano generati nuovi problemi nel mentre. 
Si mantiene così una pulizia del progetto in ogni sua fase, grazie alla continua iterazione di esse ogni volta che si incontra un problema.

Il modello a fontana è poi il primo in cui sono previste **azioni dopo la consegna**: dopo l'ultima fase (**programma in uso**), infatti, si aprono due strade, **manutenzione ed evoluzione**. La consegna non è più dunque l'atto finale, ma solo un altro step del processo, ottenendo così una **visione incrementale**.

Anche qui si perdono le garanzie sui tempi di sviluppo: una volta ritornati alla fase iniziale per risolvere un problema, non c'è la certezza di riuscire a raggiungere il punto da cui si è partiti, questo perché è possibile imbattersi in altri errori nelle fasi intermedie, costringendo un'iterazione continua per risolvere i diversi problemi. In questo modo il sw perde completamente il concetto di linearità e sarà impossibile prevederne i tempi di sviluppo, data la continua possibilità di evoluzione e manutenzione.