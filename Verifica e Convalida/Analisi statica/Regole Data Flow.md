Si può individuare la presenza di **anomalie** nell'uso delle variabili definendo certe **regole di flusso**: alcune di queste **devono necessariamente essere rispettate** in un programma corretto (**regole 1 e 3**), mentre altre hanno più a che fare con la **semantica dell'uso** di un valore (**regola 2**).

> **Non sono regole assolute**: dipende dal linguaggio classificarle come *warning* o *error*.

### Regole

#### 1. Uso

L'**uso di una variabile** deve essere **sempre preceduto** in ogni sequenza da **una definizione, senza annullamenti intermedi**.

$\color{#7CFC00}\text{Corretto}$:  $\boxed{\text d}\space \boxed{\text u}$
$\color{red}\text{Errore}$:  $\boxed{\text a}\space \boxed{\text u}$

#### 2. Definizione

La **definizione di una variabile** deve essere **sempre seguita** da **un uso, prima di un suo annullamento** o di **una nuova definizione** 

$\color{#7CFC00}\text{Corretto}$:  $\boxed{\text d}\space \boxed{\text u}$
$\color{red}\text{Errore}$:  $\boxed{\text d}\space \boxed{\text a}$ , $\boxed{\text d}\space \boxed{\text d}$

#### 3. Annullamento

L'**annullamento di una variabile** deve essere sempre **seguito da una definizione**, **prima di un uso** o altro **annullamento**.

$\color{#7CFC00}\text{Corretto}$:  $\boxed{\text a}\space \boxed{\text d}$
$\color{red}\text{Errore}$:  $\boxed{\text a}\space \boxed{\text a}$ , $\boxed{\text a}\space \boxed{\text u}$


### Riepilogo


|            | $\boxed a$                       | $\boxed d$                       | $\boxed u$                       |
| ---------- | -------------------------------- | -------------------------------- | -------------------------------- |
| $\boxed a$ | $\color{red}\text{Errore}$       | $\color{#7CFC00}\text{Corretto}$ | $\color{red}\text{Errore}$       |
| $\boxed d$ | $\color{red}\text{Errore}$       | $\color{red}\text{Errore}$       | $\color{#7CFC00}\text{Corretto}$ |
| $\boxed u$ | $\color{#7CFC00}\text{Corretto}$ | $\color{#7CFC00}\text{Corretto}$ | $\color{#7CFC00}\text{Corretto}$ |

Per riepilogare, $\boxed{a}\space \boxed{u}$ , $\boxed{d}\space \boxed{a}$ , $\boxed{d}\space \boxed{d}$ e $\boxed{a}\space \boxed{a}$ sono sequenze che identificano **situazioni anomale**, anche se non necessariamente dannose: se per esempio **usare una variabile subito dopo averla annullata** rende l'esecuzione del programma **non controllabile**, un **annullamento** immediatamente **dopo una definizione** non crea **nessun problema a *runtime***, ma è senz'altro indice di un possibile **errore concettuale**. 


### Esempio

Consideriamo la seguente funzione in $C$ con il compito di *scambiare il valore di due variabili*:
```c
void swap(int &x1, int &x2) {
    int x;
    x2 = x;
    x2 = x1;
    x1 = x;
}
```

Analizzando il codice, le **sequenze per ogni variabile** sono le seguenti:

| Variabile | Sequenza                                                            | Anomalie                                                          |
| --------- | ------------------------------------------------------------------- | ----------------------------------------------------------------- |
| `x`       | $\color{orange}\boxed{a}\space\boxed{u}$ $\boxed{u}\space\boxed{a}$ | `x` viene usata 2 volte <br>**senza essere stata prima definita** |
| `x1`      | $...\boxed{d}\space\boxed{u}\space\boxed{d}...$                     | Nessuna                                                           |
| `x2`      | $...\boxed{d}\space\color{orange}\boxed{d}\space\boxed{d}...$       | `x2` viene definita più volte senza essere usata nel frattempo    |

Come si nota, in un codice sintatticamente corretto l’**analisi Data Flow** **permette di scovare un errore semantico** osservando le *sequenze di operazioni sulle sue variabili*.