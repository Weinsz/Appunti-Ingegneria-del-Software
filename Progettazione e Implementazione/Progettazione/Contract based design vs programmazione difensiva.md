Tornando alla [[Interface segregation in azione|specificazione]] dell'interfaccia `CardSource`, si possono notare dei commenti in formato *Javadoc* che specificano **pre/post-condizioni** del metodo. Secondo il **contract-based design**, esiste un contratto tra chi implementa un metodo e chi lo chiama.

Per esempio, considerando il metodo `draw()`, **è responsabilità del chiamante** verificare il soddisfacimento delle precondizioni (_“il mazzo non è vuoto”_) prima di invocare il metodo, altrimenti ci si trova in una situazione di **violazione di contratto**.

Per specificare il contratto si possono utilizzare delle **asserzioni** (`assert`) o il `@pre` nei **commenti**. Le prime sono particolarmente utili in fase di sviluppo perché interrompono l’esecuzione del programma in caso di violazione, ma vengono solitamente rimosse in favore delle seconde nella fase di *deployment*.

Un altro approccio è la **programmazione difensiva** che al contrario delega la responsabilità del soddisfacimento delle pre-condizioni al **chiamato e non al chiamante**.