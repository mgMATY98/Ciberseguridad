##  Objetivo
Crear un entorno de laboratorio con máquinas virtuales en red interna para realizar prácticas de ciberseguridad.

Buenos dias
Para empezar deberemos de usar un entorno virtualizado debido a que, usar nuestras propias maquinas conllevaria ciertos riesgos, ademas la manipulacion de estos entornos es mucho mas sencillo
y seguro  
DESCARGA DE VIRTUAL BOX MACHINE  
Descargamos nuestro entorno virtualizado en este caso virtualBoxMachine y lo instalamos
![image](https://github.com/user-attachments/assets/b3350700-b07a-4be0-a68b-97501025da38)
Una vez hecho quedara de la siguiente manera (yo ya tengo varias maquinas virtuales instaladas):
![image](https://github.com/user-attachments/assets/ee607884-edcb-4512-bd36-8a789098f2e7)  
PASO 1:descargar ISO de kali  
Ahora procedemos a descargar e instalar nuestro Kali linux, un sistema operativo Linux repleto de herramientas muy utiles en la ciberseguridad, para ello descargaremos un ISO
de la pagina oficial de Kali Linux.  
PASO 2: instalarla en la maquina virtual  
Abrimos la VBM, vamos a nueva, y ahi podemos configurar donde se instalara la maquina virtual, el nombre y ademas el ISO a usar
![image](https://github.com/user-attachments/assets/a6e8f183-5f79-472c-abf8-3ff55ba69755)
Quedando de la siguiente forma, ya VBM nos selecciona automaticamente el tipo de SO y la version  
Luego le damos a siguiente y seleccionamos el hardware que designaremos a la maquina virtual  
![image](https://github.com/user-attachments/assets/aa0060f7-0cc4-47ff-92c0-a208e58570b1)
Luego deberemos de crear un disco virtual que usara Kali para poder operar, esto simulara un disco duro
![image](https://github.com/user-attachments/assets/52123661-64c5-46b5-80d4-8ea120083861)
Ya por ultimo le damos a termina y estaria  
PASO 3: Instalar y terminar de configurar Kali  
Aunque ya tengamos Kali en la maquina virtual es necesario una vez terminado, abrir la maquina y configurar el SO  
Entraremos a la instalacion de Kali  

Apretamos en instalacion grafica y luego elegiremos el idioma, la localizacion y el tipo de teclado

Continuamos y ya se instalara Kali  
Luego elegimos el nombre de host  

El nombre de usuario

Y la contraseña

Una vez hecho esto ya terminariamos de configurar e instalar nuestro Kali  
Para windows es exactamente igual  
PASO 4: establecer una red NAT entre la maquina windows y la kali  
Ahora bien VBM tiene muchas opciones de configuracion de red  
![image](https://github.com/user-attachments/assets/46cf469c-074f-4623-9fc3-c4a328a0f3b0)
Esta vez me centrare en red nat   
La conexion red nat es una forma de tener las maquinas virtuales conectadas entre si pero sin incluir a la maquina host, dandole mas seguridad y asi evitar que la maquina host principal se vea afectada  
Para ello vamos a:  
Herramientas-Red
![image](https://github.com/user-attachments/assets/a434b416-5479-4a2f-9414-01c2f15c5509)
Redes NAT-click derecho crear nueva red
![image](https://github.com/user-attachments/assets/a287134f-e655-404b-aa97-7a3d845f05ea)
Eso nos permitira crear redes propias para ambas maquinas y tenerlas en una red interna separada, ahora solo queda comunicarlas  
Vamos a la maquina Kali (y luego windows), seleccionamos RED, RED NAT y le asiganmos la misma red a ambas maquinas:  
![image](https://github.com/user-attachments/assets/fd0ac798-18df-41ae-abb3-6db64de55bd0)
![image](https://github.com/user-attachments/assets/74a8586f-30bc-4eb2-bae8-9a7b9564be5c)
Y ya estaria hecha la conexion entre ambas maquinas  
Ahora para verificar la conexion hacemos un ping a ambas maquinas a ver si hay respuesta  
Windows a kali:

Sin problema, ahora al reves, kali a windows

Perfecto todo configurado  
Hasta la proxima









