Il refactoring è una delle tecniche più **importanti** e **fondamentali** dell’[[eXtreme Programming (XP)]].

Non bisogna avere paura di apportare **modifiche** che semplificano il progetto: bisogna avere **coraggio**.

Il refactoring è l’operazione che **modifica solo le proprietà interne** **del software**, ad esempio la leggibilità, la semplicità e la facilità di aggiungere nuove funzioni ma **non le funzionalità stesse**.

L’obiettivo è eliminare l’entropia generata dalle continue modifiche. Il refactoring deve essere **graduale e continuo** in modo da poter aggiungere funzionalità in maniera semplice. Chiaramente, in caso di ristrutturazioni architetturali di grosse dimensioni di sistemi legacy non è sempre possibile procedere in questa maniera.

Le parti di codice che vengono aggiunte o modificate devono essere stimolate da test per garantirne la correttezza, se ciò non accade: o si aggiungono test per gestire i casi specifici, altrimenti si possono rimuovere del tutto.