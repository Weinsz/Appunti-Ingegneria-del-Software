Un test $T$ soddisfa il **criterio di copertura delle condizioni composte** se e solo se **ogni possibile composizione delle condizioni base** vale sia vero che falso per **diversi casi di test** $t \in T$.

Viene dunque testata ogni possibile combinazione di valori delle condizioni atomiche quando queste sono aggregate in condizioni composte: riprendendo per esempio la condizione `x != 0 && y < 3`, vengono testati separatamente i casi: $⟨V,V⟩, ⟨V,F⟩, ⟨F,V⟩ e ⟨F,F⟩$.

Si nota che questo criterio implica il [[Criterio di copertura delle decisioni e condizioni]], implicando a sua volta il [[Criterio di copertura delle decisioni]], [[Criterio di copertura delle condizioni|delle condizioni]] e [[Criterio di copertura dei comandi|dei comandi]].


> [!NOTE] Non applicabile
> Data la **natura combinatoria** di questo criterio, all’aumento del numero di condizioni di base **il numero di casi di test cresce però troppo rapidamente**, motivo per il quale il soddisfacimento di questo criterio è considerato **non applicabile** in pratica.

Inoltre, dato che le condizioni di base potrebbero risultare dipendenti tra loro, potrebbero esistere **combinazioni non fattibili** che non avrebbe alcun senso testare.
