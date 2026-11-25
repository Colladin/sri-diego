UT2 · Servicio DHCP de
Dato	Valor
Nombre	
Nº de orden (xx)	
Empresa	
Dominio	

    Rellena los huecos y sustituye los textos entre < >. No cambies el orden de los apartados: es el mismo que el de la lista de cotejo.

Plan de direcciones
Equipo	Hostname	MAC	Dirección IP	Cómo la obtiene
Router pfSense (LAN)	—		192.168.xx.1	Manual
Servidor DHCP	dhcp-		192.168.xx.2	Manual (fija)
Equipo de dirección (Windows)	win-			
Puesto de trabajo (Linux)	lin-			
Parámetro	Valor
Pools	
Exclusión	
Concesión / T1 / T2 (s)	
DNS del equipo de dirección	
1. Instalación del servidor · CE 2.c
E1

Qué demuestra:
2. Configuración básica · CE 2.d

La configuración completa está en kea/kea-dhcp4.conf.
E2

Qué demuestra:
E3

Qué demuestra:
E4

Qué demuestra:
3. Asignaciones dinámicas y estáticas · CE 2.e
E5

Qué demuestra:
E6

Qué demuestra:
4. Opciones adicionales · CE 2.f

Se comprueban en kea-dhcp4.conf (con el comentario junto a la reserva), E4 y E5. No hace falta nada más aquí.
5. Así funciona una solicitud · CE 2.b
E7

Qué demuestra:
Mensaje	IP origen	MAC origen	IP destino	MAC destino	Difusión o unicast
DISCOVER					
OFFER					
REQUEST					
ACK					

    xid:
    Identificador del servidor:

Renovación y caducidad (con tus tiempos, 3 o 4 líneas):
6. Informe para la empresa · CE 2.a

Tres ventajas para :

Mecanismo	Cómo obtiene el equipo su IP	Qué equipo de la oficina lo usa (en APIPA, cuándo aparece)
Configuración manual		
DHCP dinámica		
Reserva DHCP		
APIPA (169.254.x.x)		

Por qué el router y el servidor DHCP no usan DHCP:
E8

Qué demuestra:
7. Uso de IA

    No he usado IA en esta tarea.

Herramienta	Para qué la usé	Qué comprobé o corregí yo
