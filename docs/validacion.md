# Validación

## 1. VPN activa

Con el túnel IPsec activo se comprueba:

```bash
ping 10.21.68.130
traceroute 10.21.68.130
```

También se verifica el acceso HTTPS al servidor.

## 2. VPN desactivada

Se deshabilita el túnel desde la GUI de FortiGate y se repiten las pruebas.
La comunicación entre las dos redes debe dejar de funcionar.

## 3. VPN restaurada

Se vuelve a activar el túnel y se repiten las pruebas. La comunicación debe
restaurarse.
