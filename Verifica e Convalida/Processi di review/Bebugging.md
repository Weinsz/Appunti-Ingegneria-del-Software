A volte può capitare che il team di testing **non trovi errori** nel programma sotto osservazione. Oltre ad essere **scoraggiante** per chi esegue la **review** questo è spesso indice del fatto che tale attività non venga svolta in modo corretto, perché raramente un programma è proprio corretto al 100% dopo la prima scrittura.

Un metodo efficace per risolvere questo problema è il cosiddetto **bebugging**, una tecnica secondo la quale gli sviluppatori **inseriscono deliberatamente $n$ errori** nel codice prima di mandarlo in analisi al team di testing, a cui viene comunicato il numero $n$ di errori da trovare. 

> [!NOTE] Vantaggio
> L'ovvio vantaggio di questa tecnica è l'**incentivo psicologico** per il team di testing a continuare a cercare errori, facendo sì che durante la ricerca n**e vengono scovati pure molti altri non ancora noti**.

La **metrica** usata per valutare l'efficacia del testing tramite questa tecnica è dunque **la percentuale di errori trovati tra quelli inseriti intenzionalmente**, che può fornire un'indicazione della frazione di errori che il team di testing è in grado di scovare, in quanto la percentuale dei bug noti non trovati dà un'indicazione dei bug reali che rimangono. 
Se per esempio il team di sviluppo ha aggiunto 10 bug **artificiali** e durante il testing ne vengono trovati 8 più 2 non noti, si può supporre che il **team di review** riesca a trovare l'**80% degli errori** e che quindi c'è ancora un'altra porzione di **errori reali** da scovare.

Bisogna tuttavia essere molto cauti nel fare considerazioni simili: è possibile che gli errori immessi intenzionalmente siano **troppo facili o difficili** da trovare, perciò conviene sempre prendere tutto *cum grano salis*, ma almeno si trova qualcosa e non si resta a mani vuote.