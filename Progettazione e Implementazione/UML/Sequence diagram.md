Lo scopo del **diagramma di sequenza** è rappresentare il flusso di interazione tra attori all’interno di un software nel tempo. Di seguito ne è indicato un esempio:

![[Sequence.png]]

Si compone di alcuni elementi chiave:
- **attori**: rappresentano le entità coinvolte nel processo e spesso sono _oggetti_;
- **invocazioni**: identificano chiamate di metodo su un attore da parte di un altro e sono rappresentate con una freccia che va da _sinistra verso destra_. 
  **La parte a sinistra è il _chiamante_ e la parte a destra è il _chiamato_ che esegue il metodo**.
- **valori di ritorno**: visualizzati tramite una freccia tratteggiata che va da _destra verso sinistra_;
- **cicli**: aree rettangolari con l'etichetta `loop` che specificano la presenza di un ciclo in una certa zona del diagramma;
- **condizioni**: aree rettangolari con l'etichetta `opt` che specificano la necessità di verificare alcune condizioni prima di entrare nella zona corrispondente.