Ecco dunque uno **schema delle implicazioni tra i vari criteri di copertura**:

![Implicazioni tra criteri di copertura](https://marcobuster.github.io/sweng/assets/13_criteri-copertura-implicazione.png)

Come si vede, il [[Criterio di copertura delle condizioni composte]] va considerato troppo oneroso e quindi **non applicabile**, mentre gli altri criteri possono invece essere utilizzati anche nell’ambito di progetti di dimensioni reali.

I criteri visti finora **non considerano i cicli** e possono essere soddisfatti da test che percorrono il ciclo al più una volta. Molti errori però si verificano durante **iterazioni successive alla prima**, come per esempio quando si superano i *limiti di un array*.

Occorre quindi sviluppare dei criteri che tengano conto anche delle **iterazioni** e stimolino i cicli un numero di volte sufficiente:
- [[Criterio di copertura dei cammini]]
- [[Criterio di n-copertura dei cicli]]