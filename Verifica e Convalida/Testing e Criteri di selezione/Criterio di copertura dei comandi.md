Un test $T$ soddisfa il **criterio di copertura dei comandi** se e solo se ogni comando eseguibile del programma è eseguito in corrispondenza di almeno un caso di test $t \in T$.

**Metrica**: frazione di **comandi eseguiti su quelli eseguibili** dall'intero test.

Si consideri per esempio il seguente programma in pseudocodice:
#### Pseudocodice

```c
01  void main(){
02      float x, y;
03      read(x);
04      read(y);
05      if (x != 0)
06          x = x + 10;
07      y = y / x;
08      write(x);
09      write(y);
10  }
```

#### Diagramma di flusso di esecuzione
![Esempio criterio copertura comandi](https://marcobuster.github.io/sweng/assets/13_criteri-copertura-esempio-1.png)

Si può ricostruire un **diagramma di flusso di esecuzione** del codice trasformando **ogni comando in un nodo** del diagramma: **coprire tutti i comandi** vuol dire dunque **visitare tutti i nodi raggiungibili**.

Applicare il **criterio di copertura dei comandi** significa dunque trovare un insieme di casi di test in cui **per ogni nodo esiste un caso di test che lo attraversa**.

Nell'esempio il singolo caso di test $⟨3,7⟩$ risulterebbe quindi sufficiente, dato che la sua esecuzione permette di **coprire** tutti i comandi del programma.
Tuttavia, pur **massimizzando la metrica** di copertura dei comandi, tale test non è in grado di rilevare il difetto/anomalia a riga 7, in cui viene fatta una divisione senza prima controllare che il denominatore sia **diverso da zero**.

> Soddisfare il criterio di copertura dei comandi **non garantisce** dunque la **correttezza** del programma. 

Come visto infatti un'anomalia non sempre genera un malfunzionamento, perciò eseguire semplicemente tutte le righe di codice raggiungibili non assicura di rilevare eventuali errori.


 