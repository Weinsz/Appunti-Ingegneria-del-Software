#### Possibili domande che ci possiamo fare
Le [[Reti di Petri]] sono state introdotte per poter **analizzare un sistema** ancora prima di avere il codice. 
Alcune domande da porsi sono:
- Può essere raggiunta una certa marcatura?
- Può esserci una certa sequenza di scatti?
- Può esistere uno stato di deadlock?
- La rete (o una certa transizione) è viva? E di che grado?

Per rispondere a queste domande esistono diverse tecniche, suddivise in:
- **tecniche dinamiche**: ragionano sugli **stati raggiungibili** durante l’esecuzione della rete di Petri (o di un programma)
	- albero delle marcature raggiungibili (detto anche **grafo di raggiungibilità**);
	- albero di copertura delle marcature raggiungibili (detto anche **grafo di copertura**).
- **tecniche statiche** (strutturali): ragionano sulla **topologia della rete**
	- identificazione delle **$P$-invarianti** (caratteristiche invarianti riguardanti i **posti**)
	- identificazione delle **$T$-invarianti** (caratteristiche invarianti riguardanti le **transizioni**).