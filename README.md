# Write-Up-Maquina-Logic-gate
Maquina de la plataforma www.whoami-labs.com

Lo primero es iniciar la maquina vulnerable

<img width="1920" height="1140" alt="Captura de pantalla 2026-05-07 221814" src="https://github.com/user-attachments/assets/37bfbfe8-53d6-404b-8aee-ad7e41613bb1" />

# Enumeración

Una vez con la maquina iniciada Hicimos un escaneo de puertos utilizando la herramienta nmap

<img width="1920" height="1140" alt="Captura de pantalla 2026-05-07 222034" src="https://github.com/user-attachments/assets/aafbff22-8f6e-47c2-897c-3f308a7b9540" />

En vista de que la maquina contenia el puerto #22, y el puerto #80 abiertos me fui a un navegador a verificar que contenia este servidor http

<img width="1920" height="1140" alt="Captura de pantalla 2026-05-07 222115" src="https://github.com/user-attachments/assets/09e73f54-47d3-42c7-a3a7-6f165996bee1" />

En vista de que no habia nada importante fui a ver el codigo de la pagina a ver si de casualidad encontraba algo, y me lleve con la sorpresa que que habia un usuario con contraseña

<img width="1920" height="1140" alt="Captura de pantalla 2026-05-07 222205" src="https://github.com/user-attachments/assets/c8be8684-4ca4-43c5-a269-c070a20d3eec" />

# Explotación

Utilice estas credenciales para iniciar el servicio ssh a ver si tenia exito y si, lo logre

<img width="1920" height="1140" alt="Captura de pantalla 2026-05-07 222635" src="https://github.com/user-attachments/assets/9f6fc544-7c22-4cb8-bd3b-f6eb1ebe7426" />

Verifique algunos archivos

<img width="1920" height="1140" alt="Captura de pantalla 2026-05-07 222707" src="https://github.com/user-attachments/assets/971837c5-e90f-48b0-8027-8e1ebfefefe2" />

# Escalada de privilegios

Luego liste los binarios a ver si encontraba alguno que no deberia estar ahi y mucho menos con el suid activado, y encontre 3 

<img width="1920" height="1140" alt="Captura de pantalla 2026-05-07 222747" src="https://github.com/user-attachments/assets/bac48dba-dc8b-4e46-9654-972f2601557b" />

Intente enviar un comando primero el cual me diria si el coomando batcat estaba activo y si me funcionaria para leer la flag, despues de saber que estab activo le pedi que me mostrara la flag, suponiendo que podia estar en esa ubicación, y en efecto me la brindo

<img width="1920" height="1140" alt="Captura de pantalla 2026-05-07 224247" src="https://github.com/user-attachments/assets/16d36d9f-1b03-455e-841a-e9634838678b" />

Pero realmente no queria quedarme hasta ahi, sino que queria poder escalar privilegios, asi que hice el intento; primeramente intente crear un usuario y contraseña nuevo el cual tuviera privilegios root, obteniendo una respuesta positiva, es importnte recalcar que este binario "gawk" es un lenguaje de procesamiento el cual te permite leer y escribir archivos en el sistema; lo que hice con el fue darle permisos de root a traves del suid a cualquier usuario del sistema y luego de esto cree un usuario nuevo con permisos de root y una contraseña para ingresar

<img width="1920" height="1140" alt="Captura de pantalla 2026-05-07 225330" src="https://github.com/user-attachments/assets/1de54842-f102-4872-992d-bfe528967947" />

No me funciono el usuario que cree anteriormente ya que hubo un error en la escritura y la contraseña estaba mal, por lo que cree otro llamado pwn2 sin contraseña

<img width="1920" height="1140" alt="Captura de pantalla 2026-05-07 225557" src="https://github.com/user-attachments/assets/b956ffba-7534-4f8c-834a-e7fe70186207" />

Una vez creado el nuevo usuario ingrese utilizando el comando su y obtuve la sesion como root

<img width="1920" height="1140" alt="Captura de pantalla 2026-05-07 225616" src="https://github.com/user-attachments/assets/c4963f0c-7492-49a4-b122-b9018e9c3fad" />

# Resultados

Ya teniendo la sesion como root busque la flag

<img width="1920" height="1140" alt="Captura de pantalla 2026-05-07 225716" src="https://github.com/user-attachments/assets/cf9c4e18-5252-4c3a-b9bd-e7682f5c04a4" />

# MAQUINA POWNED

<img width="1920" height="1140" alt="Captura de pantalla 2026-05-07 225745" src="https://github.com/user-attachments/assets/863e2392-7b68-4769-aeb8-4fec255c0368" />

