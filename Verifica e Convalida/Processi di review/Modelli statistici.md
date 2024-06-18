Negli ultimi tempi si stanno sviluppando una serie di **modelli statistici** sulla **distribuzione degli errori** nel codice che dovrebbero teoricamente aiutare l’attività di testing guidandola verso le porzioni di sorgente che _più probabilmente_ potrebbero presentare difetti.

Tali modelli propongono infatti una **correlazione statistica** tra una serie di **metriche** quali la lunghezza del codice, il tipo di linguaggio, il grado massimo di indentazione ecc., e la **presenza ed eventuale numero di errori per categoria di errore**.

L’idea sarebbe quindi di **predire la distribuzione e il numero di errori** all’interno di uno specifico modulo del software in esame.

Occorre però **fare attenzione** alle conclusioni di queste statistiche. Utilizzare i risultati di tali modelli statistici come indicazioni sul fatto che su determinati moduli vada fatta **più attività di testing rispetto ad altri** potrebbe **inizialmente** sembrare la **soluzione più logica**. Tuttavia, tali risultati **non considerano** l’attività di testing già effettuata e le correzioni successive e quindi **non cambiano**. 
La probabilità non cambia, infatti non si fa del refactoring nel codice. Se ci sono più errori sarebbe meglio buttarli e rifarli. Dunque secondo il **modello statistico**, codice inizialmente _“scritto male”_ rimarrà **per sempre scritto male**, anche se testato estensivamente.

Con ciò in mente, si cita spesso la **Legge di Pareto/Zipf (L24)**, che viene dall'ambito economico:
> Circa l’80% dei difetti proviene dal 20% dei moduli.

Sebbene tale affermazione è indubbiamente **probabilmente vera**, è difficile sfruttare questa nozione in quanto non sono conosciuti in principio i **moduli particolarmente problematici** e il testing è comunque necessario anche in tutti gli altri.