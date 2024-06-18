Una transizione $t$ in una marcatura $M$ si dice **viva**:
- **di grado 0** (cioè **morta**): non è abilitata in $M$ e in nessuna delle marcature raggiungibili da $M$ (nessuna marcatura appartenente all'[[Insieme di raggiungibilità]]); quindi qualunque evoluzione ci sarà, la transizione $t$ non potrà mai scattare (non è sempre una cosa negativa): $$ \forall M' \in R(P/T, M)\quad \lnot M'\space[t > $$
- **di grado 1**: esiste almeno una marcatura raggiungibile da $M$ in cui la transizione $t$ è **abilitata**: $$ \exists M' \in R(P/T, M)\quad M'\space[t > $$
- **di grado 2:** per ogni numero $k$ (quindi per $k$ naturale grande a piacere) esiste almeno una sequenza di scatti ammissibile a partire da $M$ in cui la transizione scatta $k$ volte: $$ \forall k \in \mathbb N \quad M[..t..t^1..t^{k-1}..t^k> $$
- **di grado 3:** esiste almeno una sequenza di scatti ammissibile da $M$ in cui la transizione $t$ scatta infinite volte
- **di grado 4** (cioè **viva in maniera assoluta**): in qualunque marcatura raggiungibile da M, $t$ **non è morta**, quindi è possibile **far scattare la transizione almeno una volta** , di conseguenza può scattare **infinite volte in qualunque situazione** ci si trovi, ovvero in qualunque marcatura: $$  \forall M' \in R(P/T, M)\quad \exists M'' \in R(P/T, M') \quad M''\space[t >  $$

> [!NOTE] Rete viva
> Una rete viene chiamata **viva** quando tutte le sue transizioni sono **vive di grado 4**.

^638d35

### Esempio

![Esempio vitalità tranisizioni](https://marcobuster.github.io/sweng/assets/14_esempio-vitalita-transizioni.png)

- Da questo esempio pratico è possibile notare come la transizione $t_0$ è di **grado 0** in quanto non potrà mai scattare, perché è impossibile che abbia i gettoni necessari nel preset per scattare (al massimo **o in $p_0$ o in $p_1$**).
- La transizione $t_1$ è di **grado 1** perché esiste almeno una marcatura raggiungibile per cui essa scatti, infatti la marcatura corrente è quella che ne _permette_ lo scatto (ricordando ancora che se una transizione è abilitata allo scatto non significa che debba scattare).
- Osservando la transizione $t_3$ è possibile notare che essa scatti **infinite volte** (e non $n$ grande a piacere, quindi non si tratta di una transizione di **grado 2**), ma nel caso avvenga lo scatto di $t_1$ la transizione $t_3$ non potrà mai più essere abilitata (quindi esiste **una marcatura in cui non sarà possibile il suo scatto**) garantendo che **non si tratta di una transizione di grado 4**, ma bensì di **grado 3**.
- Il caso più particolare è quello della transizione t2: è noto che t3 può scattare infinite volte e quindi in p2 possono esserci infiniti gettoni; inoltre, conseguentemente allo scatto di t1 il posto p1 conterrà un gettone, ma comunque la transizione t2 non può scattare infinite volte. Questo perché è vero che all’infinito posso generare gettoni in p2, ma dal momento che scatta t1 si perde questa possibilità, permettendo a t2 di scattare tante volte quanti sono i gettoni in p2. La transazione è quindi di **grado 2**.
- Infine t4 è una transizione viva (di **grado 4**), perché qualunque sia la marcatura raggiungibile dalla marcatura corrente è possibile prendere il controllo e sicuramente esiste una sequenza di scatti tale per cui t4 diventi abilitata.