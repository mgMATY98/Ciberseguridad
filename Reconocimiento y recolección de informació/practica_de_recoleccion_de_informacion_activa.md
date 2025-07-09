A diferencia de la recoleccion pasiva, en este caso vamos a interactuar directamente con la pc objetivo, intentando adivinar su sistema operativo,
puertos abiertos, y demas informacion interesante  
Para este caso usaremos diversas herramientas para lograr nuestro objetivo:  
Herramientas usadas:  
Ping: Comando básico para verificar si el host está vivo (ICMP Echo Request).  
Netdiscover:Escanea toda la red para encontrar hosts activos mediante ARP.  
Nmap:Permite detectar puertos abiertos, servicios, versiones y sistema operativo  
Para esta práctica de recolección de información se simulará un pentest interno, ya que la mayoría de las vulnerabilidades y problemas de seguridad provienen de dentro de la organización: empleados descontentos, filtraciones de datos o malware que se propaga dentro de una PC conectada a la red interna de la empresa.  
Por ello, se configurará un entorno de laboratorio en el que mi máquina atacante (Kali Linux) y la máquina objetivo (Windows 10) están en la misma red virtual, reproduciendo así un escenario de recolección activa en un entorno interno y no externo.  
Como primer paso, debemos asegurarnos de que tanto la Kali como la Windows 10 se encuentran en la misma red, con direcciones IP dentro del mismo rango y que puedan comunicarse entre sí.  
![image](https://github.com/user-attachments/assets/17153a81-bc04-41ef-9619-b6eeb45711ef)
![image](https://github.com/user-attachments/assets/6a807761-a106-4768-89db-bcc864936cd6)
Comprobemos si se pueden comunicar entre si antes de empezar, para ello mandamos una orden de ping de una maquina a la otra:  
![ping win a kali](https://github.com/user-attachments/assets/0ed64eaa-016c-46ac-aaed-eab773d16385)
![ping kali a win](https://github.com/user-attachments/assets/a9145623-730b-46fa-8ca1-1a171a234804)
Bien ambas maquinas se reconocen y estan conectadas, empecemos.  
Paso 1: averiguar la direccion IP de mi maquina objetivo  
Para eso voy a usar la herramienta llamada Netdiscover, la cual sirve para escanear todos los dispositivos activos en la red y que me devuelva la direccion ip de cada uno de ellos, ademas voy a darle un rango propio de escaneo.  
Haciendo un ifconfig en mi maquina puedo determiar que mi direccion ip es 10.0.2.6 (dada asi por la red nat configurada previamente) por ende quiero hacer un escaneo en 10.0.2.0/16, escaneando todas las direcciones entre 0 y 16 de rango.  
![netdiscover en kali](https://github.com/user-attachments/assets/5c9666e3-a7ea-42b3-a180-a38d49257b6c)
Después de escanear la red con netdiscover, identifiqué los hosts activos en el rango 10.0.2.0/16. En este escenario aparecieron cuatro direcciones activas:  
10.0.2.1 y 10.0.2.2: direcciones del router virtual y servicios internos de VirtualBox.  
10.0.2.3 y 10.0.2.5: máquinas virtuales activas en la red.  
A continuación voy a realizar pruebas adicionales (ping y nmap) sobre ambas para confirmar cuál de ellas era la máquina Windows 10 objetivo. En un entorno real esto se hace observando los servicios detectados y los puertos abiertos característicos del sistema operativo del objetivo.  
Paso 2: hacer un ping a las ip de los host descubiertos para ver si estan activos  
![pingVerificacion](https://github.com/user-attachments/assets/5c99a8d5-b7f7-4541-8247-eec37cc362d7)
Al estar ambos host activos no puedo identificar a mi objetivo, para determinar cuál de ellos corresponde a la máquina objetivo, realizare un escaneo activo de puertos utilizando nmap para ver los puertos y servicios activos.  
![Nmap](https://github.com/user-attachments/assets/18351c16-bfa9-4a7d-9271-6933ee40d77f)
La IP 10.0.2.3 no mostró ningún puerto abierto conocido y todos los puertos TCP reportaron estado filtered, lo que indica que no hay servicios comunes accesibles. Esto no coincide con el comportamiento esperado para una maquina activa, ya que por defecto no tiene servicios escuchando.  
La IP 10.0.2.5 presentó puertos abiertos típicos de un sistema Windows:

135/tcp (msrpc): Remote Procedure Call.  

139/tcp (netbios-ssn): NetBIOS Session Service.  

445/tcp (microsoft-ds): Microsoft Directory Services (SMB).  

Por lo tanto, se determinó que la IP 10.0.2.5 corresponde a la máquina Windows 10 objetivo.  
Paso 3: hacer un escaneo de profundidad con nmap para ver mas datos sobre el objetivo.  

