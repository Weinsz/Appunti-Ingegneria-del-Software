Si studiano le **reti di Petri** come esempio di **linguaggio formale**: [[Processo di produzione del software|fin dai primi argomenti]] è stato possibile apprendere come l'ingegneria del sw si occupi di linguaggi e comunicazione.

Partendo infatti dai [[Processo di produzione del software|processi]] che sfruttano un linguaggio poco formale e con poca terminologia tecnica (ad esempio le *user story*) e passando per la [[Progettazione]] in cui è stato usato un linguaggio più rigoroso, si arriva a un vero linguaggio formale utile a **raccogliere delle specifiche**.

Esiste un **modello standard di rete di Petri** e delle **possibili estensioni** di quest’ultimo, ad esempio alcuni possibili dialetti come le [[Reti temporizzate]], utili a descrivere **sistemi real time** che necessitano di requisiti formali per ridurne le criticità.

In generale usare linguaggi complessi e formali per descrivere le specifiche può essere **costoso**: vengono infatti usati principalmente in **contesti critici**, dove i fallimenti provocano conseguenze molto gravi (classico esempio: *la centrale nucleare esplode*) e in cui la **sicurezza deve essere garantita** prima di mettere in funzione il software.

Le **reti di Petri** sono in parte simili agli **automi a stati finiti** (FSM) ma specificatamente **nascono per descrivere sistemi concorrenti**. Tra gli altri aspetti, i concetti di *stato e transizione* per le reti di Petri differiscono rispetto a quelli già noti per le FSM:
- lo **stato** nelle reti non è più un'informazione atomica vista a livello di sistema, ma come **composizione** di tante parti diverse (**stati parziali**);
- le **transizioni** (promosse a **nodi** invece di semplici archi), di conseguenza, non operano più quindi su uno stato globale, ma si limitano a **variarne una parte**.

Nelle **FSM** esiste un **unico stato attivo** e gli **stati disponibili** sono dati dal *prodotto cartesiano* di tutti i possibili valori delle diverse entità. 
Per contro, nelle **reti di Petri** ci sono **diversi stati attivi** in un dato momento, permettendo di semplificarne notevolmente la rappresentazione e l'[[Analisi delle reti di Petri|analisi]].

Si vanno a vedere in dettaglio:
- [[Definizioni delle reti]]
- [[Macchine a stati finiti]]
- [[Relazioni tra transizioni]]
- [[Insieme di raggiungibilità]]
- [[Limitatezza]]
- [[Vitalità di una transizione]]
- [[Capacità dei posti]]
- [[Archi inibitori]]
- [[Eliminazione pesi sugli archi]]
- [[Conservatività]]
- [[Stato base e rete reversibile]]