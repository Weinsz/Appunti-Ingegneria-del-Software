Prima di studiare i pattern, è bene chiedersi come poter parlare di design pattern: lo si fa mediante i [_meta-pattern_](https://web.archive.org/web/20170809131649/http://www.info.uni-karlsruhe.de/~i44www/lehre/swk/2003SS/Papiere/ECOOP1994-Pree-Metapatterns.pdf), cioè pattern con cui costruire altri pattern.

Nello specifico, i meta-pattern identificano **2 elementi base** su cui ragionare quando si trattano i pattern:
- **Hook Method**: è un *metodo astratto* che, implementato, **determina il comportamento specifico** nelle sottoclassi; è il **punto caldo** su cui si interviene per adattare lo schema alla situazione.
- **Template Method**: è una struttura generale che **contiene delle parti cambiabili**, cioè gli **hook**; dunque è il metodo che coordina generalmente più **Hook Method** per realizzare il design desiderato. Si tratta del punto/**elemento freddo** di invariabilità del pattern che ne realizza la rigida struttura.

**Struttura**:
- Template Method (parte fredda)
	1. Hook (parte calda)
	2. Hook
	3. ...

Un esempio può essere una funzione di **ordinamento**, in cui c'è uno scheletro generale dell'algoritmo (*template*) al cui interno non viene specificata la modalità di comparazione tra elementi. Modificando questa comparazione si realizzano gli *hook* che, se inseriti dentro 
il *template*, rendono l'algoritmo funzionante.   

I metodi **template** devono avere un modo per accedere ai metodi **hook** se intendono usarli per realizzare i pattern. Questo collegamento può essere fatto in 3 modi differenti:
1. **Unification**: *hook* e *template* si trovano nella **stessa classe astratta**, da cui erediteranno le classi concrete per implementare i metodi *hook* e quindi di conseguenza il pattern; i metodi *template* sono invece già implementati in quanto la loro struttura non deve adattarsi alla specifica applicazione. 
   Un esempio è presente nell'interfaccia **`Iterator`** (pattern [[Iterator]]), che richiede l'implementazione dei metodi `next()` e `hasNext()` (inoltre è presente un metodo di default `forEach()` che permette di chiamare next fintantoché hasNext dà True). La struttura generale che vale sempre (*template*) è data dal metodo `forEach()`, mentre gli *hook* invece sono `next()` e `hasNext()`, che se forniti permettono al template di funzionare.

> [!NOTE] Dove viene applicato
>    **Questo tipo di relazione viene adottata anche dal pattern [[Singleton]].**

   [![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/692394f1e3c96d328e8154db45840a697dc4f08d.svg)
2. **Connection**: *hook* e *template* sono in **classi separate**, indicate rispettivamente come *hook class* (astratta) e *template class* (concreta, dato che rimane), collegate tra di loro da
   un'**associazione** (prima era segnata aggregazione, il prof nella rec dice l'altra, ma la rappresenta come aggregazione): la classe *template* contiene cioè un'istanza della classe *hook*, in realtà, un'istanza della classe concreta che implementa i metodi *hook* usati per realizzare il pattern. Dunque in base all'implementazione dell'hook il comportamento generale cambia.

> [!NOTE] Dove viene applicato
> **Questo tipo di relazione viene adottata anche dal pattern [[Strategy]].**
   
   [![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/3356b1282ead55458e538c62bf1a17c1f86f97a1.svg)
3. **Recursive connection:** come nel caso precedente _hook_ e _template_ sono in classi separate, ma oltre all'**associazione/aggregazione**, tali classi sono legate anche da una relazione di **generalizzazione**: la classe *template* è una classe *hook*. Le relazioni tra le due classi sono **doppie e magari ricorsive**. 

> [!NOTE] Dove viene applicato
> **Questo tipo di relazione viene adottata dai pattern [[Decorator]], [[Composite]]
> e [[Chain of responsibility]].**

[![](https://marcobuster.github.io/sweng/mdbook-plantuml-img/7edc9ec858f935e7f0441e2c39991d9dd49c693b.svg)