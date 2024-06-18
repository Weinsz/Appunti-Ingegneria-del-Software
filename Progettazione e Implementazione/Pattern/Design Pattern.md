Parlando di [[Progettazione]] del software e di buone pratiche non si può non parlare di **design pattern**, che sono soluzioni universalmente riconosciute valide a problemi di design ricorrenti: si tratta cioè di **strumenti concettuali** di progettazione (**non codice**) che esprimono una buona architettura del sw **catturando la soluzione ad una famiglia di problemi**. 
Ogni pattern deve avere un nome il più possibile evocativo, in modo da favorirne la memorizzazione, ovvero che permetta di riconoscere subito i casi in cui adottarlo.

Ad ogni pattern sono associati una serie di **idiomi**, ovvero delle implementazioni del pattern specifiche per un certo linguaggio che sfruttano i suoi costrutti per realizzare l’architettura dettata dal pattern (ciò implica che non sono utilizzabili in tutti i linguaggi). Si vedranno alcuni idiomi per Java, che a volte si discosteranno molto dalla struttura descritta dai diagrammi [[UML]] dei pattern.

Ma esistono anche degli **anti-pattern**, spesso mostrati assieme al pattern come dimostrazione della sua correttezza. Si tratta di soluzioni che _inizialmente sembrano_ buone ma si può dimostrare siano problematiche: bisogna assicurarsi di tenersi lontani da questi design negativi.

I pattern che vedremo fanno parte dei cosiddetti “**Gang Of Four (GoF) Patterns**”, una serie di 23 pattern definiti da Erich Gamma, Richard Helm, Ralph Johnson e John Vlissides, ormai molti anni fa ma ancora attuali. 
Oltre ad averli definiti li hanno divisi in 3 categorie:
- **Creazionali**: legati alla **creazione di oggetti**
- **Comportamentali**: legati all’**interazione tra oggetti**
- **Strutturali**: legati alle **composizioni di classi e oggetti**

### Indice
- [[Meta-pattern]]
- **Pattern Creazionali**
	- [[Singleton]]
	- [[Factory Method]]
	- [[Abstract Factory]]
	- [[Builder]]
- **Pattern Strutturali**
	- [[Flyweight]]
	- [[Adapter]]
	- [[Façade]]
	- [[Composite]]
	- [[Decorator]]
- **Pattern Comportamentali**
	- [[Iterator]]
	- [[Chain of responsibility]]
	- [[Null Object]] (non fa parte dei pattern GoF)
	- [[Strategy]]
	- [[Observer]]
	- [[State]]
- [[Model View Controller (MVC)]]
- [[Model View Presenter (MVP)]]
