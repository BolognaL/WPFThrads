# DIARIO WPFThreads

## Scopo del compito

Il risultato finale era quello di realizzare un conteggio prevedendo 3 oggetti TextBlock WPF che visualizzavano l'avanzamento di tre contatori diversi.

Il primo scatta ogni ms o conta fino a 5000, il secondo scatta ogni 10 ms e conta fino a 500 mentre l'ultimo scatta ogni 100 ms e conta fino a 50. Ogni contatore dura 5 secondi.

Contemporaneamente a questi 3 conteggi ce ne deve essere un quarto che tenga conto del conteggio finale.

Per far partire i threads contatori deve essere prensente un pulsante Start che rimanga disattivato fino alla fine dei conteggi.

L'ultimo punto (opzionle) era quello di far visualizzare il conteggio finale tramite una ProgressBar


### Codice che utilizza il costrutto lock e il metodo Dispatcher.invoke

![cattura](/images/Cattura1.PNG)

Creando “incrementa2” abbiamo creato un altro processo che contatore indipendente dall’altro. In modo tale da non interferire con l'altro conteggio

### Metodi del semaforo

Il semaforo non può essere assolutamente negativo; esso può avere 2 funzioni: 


![cattura](/images/Cattura2.PNG)   signal() ⇒ La funzione signal viene utilizzata per rilasciare il controllo del semaforo. Quando un processo o thread ha finito di utilizzare la risorsa condivisa, invoca la funzione signal per incrementare il valore del semaforo. Questo permette ad altri processi o thread in attesa di acquisire il controllo del semaforo e accedere alla risorsa condivisa.

![cattura](/images/Cattura3.PNG)   wait() ⇒ La funzione wait viene utilizzata per acquisire il controllo del semaforo. Se il valore del semaforo è maggiore di zero, il processo o thread può accedere alla risorsa condivisa e decrementare il valore del semaforo. Altrimenti, il processo o thread viene messo in attesa finché il valore del semaforo non diventa maggiore di zero. In pratica, il processo o thread che invoca la funzione wait viene bloccato fino a quando il semaforo non diventa disponibile.

### Codice per inizializare un semaforo

![cattura](/images/Cattura.PNG)

![cattura](/images/Cattura6.PNG)

Quando un thread è partito non si possono far partire anche gli altri perché altrimenti il semaforo precedente viene distrutto.

Non si puo utilizzare un semaforo all’interno di un event handler per questo dobbiamo creare un altro thread

### Codice per il metodo Dispatcher.invoke()

![cattura](/images/Cattura5.PNG)

In questa maniera utilizzando il metodo “Dispatcher.Invoke” riusciamo a far collaborare i 2 threads contemporaneamente in modo tale che il programma non si blocchi.
Invoke ha dei parametri lambda expression ⇒ codice da eseguire. lo possiamo anche mettere come parametro ad un thread da eseguire
