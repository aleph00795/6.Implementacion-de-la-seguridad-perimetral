https://learn.microsoft.com/es-mx/training/modules/perimeter-security/1-introduction

## Emparejamiento de redes virtuales
Este laboratorio requiere dos máquinas virtuales, cada una de las cuales debe estar en una red virtual diferente. Para estas instrucciones, tenemos AZ500vm01, AZ500vm02, AZ500-vnet, AZ500-vnet1 y az500-rg.

Si quiere ahorrar tiempo, puede conectarse a cada máquina virtual. Además, puede resultar útil editar la página default.htm en cada máquina, de manera que la página proporcione el nombre de la máquina virtual. Por ejemplo, esta es AZ500vm01.

En esta demostración, configurará y probará el emparejamiento de VNet.

### Revisión de la configuración de la infraestructura

En esta tarea, revisará la infraestructura que se configuró para esta demostración.

1. En el Portal, vaya a Máquinas virtuales.

2. Verá dos máquinas virtuales, AZ500vm01 y AZ500vm02.

3. Seleccione AZ500vm01 y revise las direcciones IP.

4. Seleccione AZ500vm02 y revise las direcciones IP. Anote la dirección IP privada.

5. En función del direccionamiento, analice cómo se encuentra cada máquina en una subred diferente.

6. En el Portal, vaya a Redes virtuales.

7. Verá dos redes virtuales, AZ500-vnet y AZ500-vnet1.
