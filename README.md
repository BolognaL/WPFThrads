# DIARIO WPFThreads

## Scopo del compito

Il risultato finale era quello di realizzare un conteggio prevedendo 3 oggetti TextBlock WPF che visualizzavano l'avanzamento di tre contatori diversi.

Il primo scatta ogni ms o conta fino a 5000, il secondo scatta ogni 10 ms e conta fino a 500 mentre l'ultimo scatta ogni 100 ms e conta fino a 50. Ogni contatore dura 5 secondi.

Per far partire i trce contatori deve essere prensente un pulsante Start che rimanga disattivato fino alla fine dei conteggi. 


### Codice che utilizza il costrutto lock e il metodo Dispatcher.invoke

![cattura](/images/Cattura1.PNG)

Creando “incrementa2” abbiamo creato un altro processo che conta ed è indipendente dall’altro.

### Metodi del semaforo

Il semaforo non può essere assolutamente negativo; esso può avere 2 funzioni: 


![cattura](/images/Cattura2.PNG)   signal() ⇒ (decrementa il contatore e quando arriva a 0 si ferma)

![cattura](/images/Cattura3.PNG)   wait() ⇒ (è una procedura bloccante)

### Codice per inizializare un semaforo

![cattura](/images/Cattura.PNG)

![cattura](/images/Cattura6.PNG)

Quando un thread è partito non si possono far partire anche gli altri perché altrimenti il semaforo precedente viene distrutto.

Non si puo utilizzare un semaforo all’interno di un event handler per questo dobbiamo creare un altro thread

### Codice per il metodo Dispatcher.invoke()

![cattura](/images/Cattura5.PNG)

In questa maniera utilizzando il metodo “Dispatcher.Invoke” riusciamo a far collaborare i 2 threads contemporaneamente in modo tale che il programma non si blocchi.
Invoke ha dei parametri lambda expression ⇒ codice da eseguire. lo possiamo anche mettere come parametro ad un thread da eseguire
