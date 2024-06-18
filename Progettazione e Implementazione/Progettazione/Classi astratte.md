Una **classe astratta** che implementa un’interfaccia **non deve necessariamente implementarne tutti i metodi**, ma può delegarne l’implementazione alle sottoclassi impedendo l’istanziamento di oggetti del suo tipo.

Le **interfacce** diminuiscono leggermente le performance, però **migliorano estremamente la generalità**, che aiuta l’espandibilità ed evolvibilità del programma. È possibile utilizzare le **classi astratte** anche per classi complete, ma che **non ha senso che siano istanziate**. Un buon esempio sono le classi _utility_ della libreria standard di Java.

#### Classe utility della libreria standard di Java
- **`Collections.shuffle(List<?> list)`**
- **`Collections.sort(...)`** con la seguente signature:
```java
public static <T extends Comparable<? super T>> void sort(List<T> list)
```
Cioè sort ha bisogno che gli elementi della lista da ordinare implementino `Comparable`, e quindi siano confrontabili tra di loro. Inoltre `Comparable` è un altro esempio di [[Interface segregation]]: serve per specificare che un oggetto ha bisogno della caratteristica di essere comparabile.

La classe `Collections` era l’unico modo per definire dei metodi sulle interfacce (es: dare la possibilità di avere dei metodi sulle collezioni, cioè liste, mappe, ecc.), ma ora si possono utilizzare i **metodi di default** nelle interfacce.