![Schema git](https://marcobuster.github.io/sweng/assets/05_git-schema.png)

In figura, possiamo osservare 4 **livelli** ordinati:
- **working directory** (WD): rappresenta la _configurazione_ della directory di lavoro sul filesystem, esiste indipendentemente da git. Può essere vista come l’unione dei _tracked_ and _untracked_ files;
- **index** (o **area di staging**): insieme dei _tracked_ files da git.
- (n?) **local repository**: insieme delle modifiche committate e relativo storico.
- (n) **remote repository**: branch remoto, è possibile avere sia più branch per progetto remoto che più progetti remoti configurati.

Il termine _**repository**_ è abbastanza ingannevole, perché è comunemente associato ad un progetto mentre in quest'astrazione a livelli corrisponde di fatto a un **branch**.

Il passaggio tra un livello e l’altro non è mai automatico, ma è sempre esplicitato da un’operazione.

![Puntatori commit git](https://marcobuster.github.io/sweng/assets/05_git-commits.png)

Per ogni branch c’è un puntatore all’ultimo commit di tale branch. L’HEAD punta all’ultimo commit in cui siamo: normalmente corrisponde al puntatore del branch corrente; quando non è così siamo in una situazione di _HEAD scollegato_. È utile potersi spostare tra i commit per controllare revisioni precedenti.

#### `git merge` — _join two or more development histories together_

Il comando `git merge` è utile per unire branch (o più in generale alberi) insieme nel branch corrente.

Se i due branch non sono divergenti, il merge avviene in modo banale con un _fast-forward_: nessun ulteriore commit verrà cambiato, verrà solo modificato il puntatore del branch e l’HEAD. Per forzare la creazione di un merge di commit (in [[GitFlow]] è apprezzato) occorre utilizzare 
l’opzione `--no-ff`.

In tutti gli altri casi, il merge può concludersi con successo oppure possono avvenire dei conflitti. Una volta risolti tutti i conflitti è sufficiente commitare le modifiche concludendo quindi il merge.