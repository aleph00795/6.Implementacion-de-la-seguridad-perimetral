https://learn.microsoft.com/es-mx/training/modules/perimeter-security/1-introduction

## Emparejamiento de redes virtuales
Este laboratorio requiere dos máquinas virtuales, cada una de las cuales debe estar en una red virtual diferente. Para estas instrucciones, tenemos AZ500vm01, AZ500vm02, AZ500-vnet, AZ500-vnet1 y az500-rg.

Si quiere ahorrar tiempo, puede conectarse a cada máquina virtual. Además, puede resultar útil editar la página default.htm en cada máquina, de manera que la página proporcione el nombre de la máquina virtual. Por ejemplo, esta es AZ500vm01.

![image](https://user-images.githubusercontent.com/110675810/192394514-9a1cc0c1-2268-4aa4-be86-d87649776bb1.png)

![image](https://user-images.githubusercontent.com/110675810/192394334-75e0138e-dd16-4e90-9bd0-38dfe7b747c7.png)

En esta demostración, configurará y probará el emparejamiento de VNet.

### Revisión de la configuración de la infraestructura

En esta tarea, revisará la infraestructura que se configuró para esta demostración.

1. En el Portal, vaya a Máquinas virtuales.

2. Verá dos máquinas virtuales, AZ500vm01 y AZ500vm02.

![image](https://user-images.githubusercontent.com/110675810/192394637-355b2c7d-d68b-4452-bc6c-040a96bf9958.png)

3. Seleccione AZ500vm01 y revise las direcciones IP.

![image](https://user-images.githubusercontent.com/110675810/192395446-adbc4bd4-186d-4528-a87d-d51f7d2fe3fc.png)

4. Seleccione AZ500vm02 y revise las direcciones IP. Anote la dirección IP privada.

![image](https://user-images.githubusercontent.com/110675810/192395653-eeb5313a-2982-4b01-af80-6d220cf163ad.png)

5. En función del direccionamiento, analice cómo se encuentra cada máquina en una subred diferente.

6. En el Portal, vaya a Redes virtuales

7. Verá dos redes virtuales, AZ500-vnet y AZ500-vnet1.

![image](https://user-images.githubusercontent.com/110675810/192396756-4bfb05ff-8dc5-4a50-9ad7-5fb6d6bca521.png)

### Prueba de las conexiones de máquina virtual

En esta tarea, probará la conexión de AZ500vm01 a la dirección IP privada de AZ500vm02. Esta conexión no funcionará. Las máquinas virtuales están en redes virtuales diferentes.

1. Utilice RDP para conectarse a AZ500vm01.

2. En un explorador, vaya a la página http://localhost.default.htm.

3. Esta página debe mostrarse sin errores.

![image](https://user-images.githubusercontent.com/110675810/192398246-adad8892-519a-4d78-971c-42ba69b0be35.png)

4. Utilice RDP para conectarse a AZ500vm02.

5. En un explorador, vaya a la página http://localhost.default.htm.

6. Esta página debe mostrarse sin errores.

![image](https://user-images.githubusercontent.com/110675810/192398307-dda49ee8-35ae-476f-8e80-cdcddc488c3b.png)

7. Los pasos anteriores muestran que IIS funciona en las máquinas virtuales.

8. Vuelva a la sesión de RDP para AZ500vm01.

9. Ahora intentaremos acceder a AZ500vm02.

10. En un explorador, vaya a la página http://private_IP_address_of_AZ500vm02/default.htm.  

http://10.1.0.4/default.htm

11. No se mostrará la página.

12. AZ500vm01 no puede acceder a AZ500vm02 mediante la dirección privada.

![image](https://user-images.githubusercontent.com/110675810/192398708-400b32ce-df44-4e02-884c-2c4147a15355.png)

### Configuración del emparejamiento de VNet y prueba de las conexiones

En esta tarea, configurará el emparejamiento de VNet y probará la conexión anterior. La conexión ahora funcionará.

1. En el Portal, vaya a la red virtual AZ500-vnet.

2. En Configuración, seleccione Emparejamientos.

![image](https://user-images.githubusercontent.com/110675810/192398961-0502e861-79f8-42ae-981a-82be24146109.png)

3. + Agregue un emparejamiento de red virtual. La página se adapta a medida que realiza algunas selecciones.

![image](https://user-images.githubusercontent.com/110675810/192399054-956b2262-a797-4510-8a87-1f1f95a09275.png)

- Nombre del emparejamiento de az500-vnet a la red virtual remota: Peering-A-to-B
- Red virtual: AZ500-vnet1 (az500-rg)
- Nombre del emparejamiento de az500-vnet1 a az500-vnet: Peering-B-to-A
- Analice las otras opciones de configuración.
- Haga clic en OK.

4. Siga las notificaciones mientras se implementan los emparejamientos de red virtual.

![image](https://user-images.githubusercontent.com/110675810/192399615-93ffcef7-501f-402e-9db7-221fa9aad13f.png)

5. Vuelva a la sesión de RDP para AZ500vm01.

6. En el explorador, actualice la página http://private_IP_address_of_AZ500vm02/default.htm.

http://10.1.0.4/default.htm

7. Ahora debería verse esta página.

![image](https://user-images.githubusercontent.com/110675810/192399733-3d37db17-8ec1-4b65-a383-7988dd9f0449.png)

## Azure Firewall
Esta tarea requiere una red virtual con dos subredes, Subnet1 y Jumpnet. Subnet1 tiene el intervalo de direcciones 10.0.0.0/24. Jumpnet tiene el intervalo de direcciones 10.0.1.0/24. Subnet1 incluye una máquina virtual Windows. Los nombres de los recursos pueden ser diferentes.

### Configuración de la subred del firewall

1. En el Portal, seleccione la red virtual.

2. En Configuración, seleccione Subredes.

![image](https://user-images.githubusercontent.com/110675810/192400178-7692f2e2-bf4b-4740-8ea2-43116fb57cdb.png)

3. Haga clic en + Subred para agregar una subred nueva para el firewall.

- Nombre: AzureFirewallSubnet
- Intervalo de direcciones: 10.0.2.0/24
- No se necesita una instancia de NAT Gateway, un grupo de seguridad de red, una tabla de enrutamiento ni servicios.
- Haga clic en Agregar.

![image](https://user-images.githubusercontent.com/110675810/192400273-bcff1492-86c9-4d65-a01f-de094375d4f4.png)

4. Espere a que se implemente la subred.

![image](https://user-images.githubusercontent.com/110675810/192400382-c106a0c0-fec4-478b-abf1-c55a99fe8dc4.png)

### Incorporación y configuración del firewall

1. Busque Firewalls y seleccione la opción.

2. Analice las ventajas de un firewall y cómo se puede usar para aumentar la seguridad perimetral.

3. Haga clic en + Agregar.

4. Complete la información de configuración necesaria: suscripción, grupo de recursos, nombre y región.

5. Seleccione la red virtual.

6. Agregue una IP pública de firewall nueva.

7. Cree el firewall y espere a que se implemente.

![image](https://user-images.githubusercontent.com/110675810/192401245-9d8536e5-ac3f-4674-911a-949cfa019fcf.png)

8. Vaya al firewall nuevo.

![image](https://user-images.githubusercontent.com/110675810/192402041-a55ea132-cce5-4763-9bc1-cfdb0bb830e7.png)

9. En la hoja Información general, ubique la IP privada del firewall.

10. Copie la dirección en el Portapapeles.

10.0.1.4

### Creación de una tabla de enrutamiento y la ruta que utiliza el firewall

1. Busque y seleccione Tablas de rutas.

![image](https://user-images.githubusercontent.com/110675810/192402147-be3ddca5-6daa-485d-950a-32843a43077f.png)

2. Agregue una tabla de enrutamiento nueva.

3. Complete la información de configuración necesaria: nombre, suscripción, grupo de recursos y ubicación.

![image](https://user-images.githubusercontent.com/110675810/192402254-b246899a-ff1d-4824-bde1-8228541f01a7.png)

4. Deshabilite la opción Propagación de rutas de puerta de enlace de red virtual. Revise lo que significa esto.

5. Cree la tabla de enrutamiento y espere a que se implemente.

6. Vaya a la tabla de enrutamiento nueva.

![image](https://user-images.githubusercontent.com/110675810/192402386-d0f41e32-b01a-43ab-bd13-de8dba208af2.png)

7. En Configuración, haga clic en Rutas.

![image](https://user-images.githubusercontent.com/110675810/192402426-5add959a-04d6-4cbf-8347-a8fe6e2210ad.png)

8. Agregue una ruta nueva. Esta ruta garantizará que el tráfico pase por el firewall. Analice los diferentes tipos de próximo salto.

- Nombre de la ruta: su elección
- Prefijo de dirección: 0.0.0.0/0/
- Tipo de próximo salto: aplicación virtual
- Dirección de próximo salto: dirección_IP_privada_del_firewall

![image](https://user-images.githubusercontent.com/110675810/192402749-12245c3e-95cb-4242-80f3-5a4e49bb3e25.png)

9. Cuando termine, haga clic en Aceptar y espere a que se implemente la ruta nueva.

![image](https://user-images.githubusercontent.com/110675810/192402806-e1e6e367-0c8d-47b6-9b69-335d53c491ea.png)

### Asociación de la tabla de enrutamiento con Subnet1

1. Todavía en el recurso de la tabla de enrutamiento, en Configuración, haga clic en Subredes.

![image](https://user-images.githubusercontent.com/110675810/192402889-b3b97126-47bf-4346-a540-cc8cb5f844f8.png)

2. Asocie la red virtual y Subnet1. Esto garantizará que Subnet1 use la tabla de rutas.

3. Cuando termine, haga clic en Aceptar y espere a que se complete la asociación.

![image](https://user-images.githubusercontent.com/110675810/192403468-7f4dc987-95ea-4619-b609-f77387b064d4.png)

### Probar el firewall

1. En el Portal, vaya a una máquina virtual en Subnet1.
2. En la hoja Información general, asegúrese de que la VM esté en ejecución.
3. Haga clic en Conectar y establezca una conexión del Protocolo de escritorio remoto con la VM.
4. Abra un explorador en la máquina virtual.
5. Intente acceder a: www.msn.com.
6. Observe el error. Se deniega la acción. No hay concordancia de reglas.


### Incorporación de una regla de aplicación de firewall

1. En el Portal, vaya al firewall.

2. En Configuración, seleccione Reglas.

3. Seleccione la pestaña Selección de reglas de aplicación.

4. Haga clic en Agregar una colección de reglas de aplicación.

5. Revise cómo funcionan las reglas de aplicación y complete la información necesaria.

- Nombre: su elección
- Prioridad: 300
- Acción: Permitir

6. Siga completando la regla en FQDN de destino. Esto permitirá que la dirección IP de Subnet1 atraviese el firewall.

- Nombre: Allow-MSN
- Tipo de origen: dirección IP
- Origen: 10.0.0.0/24
- Protocolo: puerto: http,https
- FQDN de destino: www.msn.com

7. Haga clic en Agregar y espere a que se actualice el firewall

### Otra prueba del firewall

En la sesión de RDP de la máquina virtual, actualice la página del explorador.
Ahora debería verse la página MSN.com.

