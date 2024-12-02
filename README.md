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

## Disminuir la versión de Opencv
![image](https://github.com/user-attachments/assets/66d7c495-ec85-4718-bbed-ee6beeb63221)

Em este momento si instalas opencv usando pip install lo harás con la version 4.10.0
Vamos a intentar ir a una version anterior mas estable.

Cabe anotar que esto no ocurría cuando en el repositorio de cliente controlled de valkiria se trabajaba con el FOURCC por defecto, esta
falla aparece utilizando estos settings

>    def load_default_settings(self):
        TARGET_WIDTH = 1280
        TARGET_HEIGHT = 720
        FOURCC = "MJPG"
        MAX_FRAME_RATE = 22
        # Set the camera resolution to the target panoramic width and height
        self.cap.set(cv2.CAP_PROP_FRAME_WIDTH, TARGET_WIDTH)
        self.cap.set(cv2.CAP_PROP_FRAME_HEIGHT, TARGET_HEIGHT)
        self.cap.set(cv2.CAP_PROP_FOURCC, cv2.VideoWriter_fourcc(*FOURCC))
>        self.cap.set(cv2.CAP_PROP_FPS, MAX_FRAME_RATE)


https://github.com/opencv/opencv/issues/25736 with newest version 
https://github.com/opencv/opencv/issues/20311 with older versions 

### Uninstall Opencv
> pip uninstall opencv-python 
> pip uninstall opencv-python-headless

### Reinstall Opencv Targeting older version
> pip install opencv-python==4.4.0.46 
> pip install opencv-python-headless==4.4.0.46 

## SetUp Git Permissions using ssh
https://chatgpt.com/share/66ffd2af-13d0-8005-912a-e611c7df3c69
 

# Valkiria 25 Migration

## Raspberry controlled code update

The raspberry was last in a branch called raspberry-modf
I am about to make any git neccesarry step to update to the branch servipy-impl which is the one containing the merge-code.

Later a new branch reorganization will be required!