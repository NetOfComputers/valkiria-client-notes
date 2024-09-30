# valkiria-client-notes

La raspberry funciona dentro de un recipiente hermético, por lo que la temperatura general del SBC es una variable MUY a tener en cuenta. Sin embargo he visto 
que cuando varias tareas del modelo de arquitectura de valkiria engines son lanzadas contra el cliente, entonces se queda bloqueado hasta pasados unos minutos.

Tanto en su estado de reposo como en maxima carga el swap memmory o swp tiene este aspecto ![image](https://github.com/user-attachments/assets/27599ae2-1083-44b1-8e37-4cb3a72e35fd)

Utilizaré este archivo para recoger las diferentes aplicaciones que he cometido a la raspberry para optimizar su tarea para el caso concreto


## Aumentar SwapSpace

- Usando comandos como htop si observamos un uso muy elevado de RAM y SWP podemos tratar de aumentar el SWP(memoria fisica como memoria de cpu) esto no es ideal, pero lo es menos
- carecer de memoria suficiente

> sudo dphys-swapfile swapoff  # Turn off the current swap  
> sudo nano /etc/dphys-swapfile  # Edit the swap file size (e.g., change 100M to 1G)  
> sudo dphys-swapfile setup  # Set up the new swap file  
> sudo dphys-swapfile swapon  # Turn swap back on  

Quedaría en mi caso algo como lo siguiente al poner 650
![image](https://github.com/user-attachments/assets/fd1bc95c-6b59-4597-b11a-c8c15b428b16)
