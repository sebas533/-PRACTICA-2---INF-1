# Práctica #2 — Topología #1: VPN Site-to-Site con FortiGate

## Descripción

Implementación de una infraestructura de red con dos FortiGate, un enlace ISP,
una red de usuarios mediante VLAN 10 y un servidor web HTTPS. La comunicación
entre la red de usuarios y el servidor se realiza mediante una VPN IPsec
Site-to-Site.

## Objetivos

- Configurar la infraestructura de red mediante GUI en FortiGate.
- Configurar VLAN 10 y DHCP para los usuarios.
- Configurar NAT.
- Configurar una VPN IPsec Site-to-Site entre los FortiGate.
- Implementar un servidor Web mediante HTTPS.
- Comprobar la conectividad mediante ping y traceroute.
- Comprobar que la comunicación depende del túnel VPN.

## Topología

> Coloca aquí la captura de la topología:
> 

## Plan de direccionamiento

| Equipo | Función | Dirección |
|---|---|---|
| ISP | WAN hacia FG1 | `21.68.1.1/30` |
| FG1 | WAN | `21.68.1.2/30` |
| FG1 | VLAN 10 / Gateway | `10.21.68.1/25` |
| Usuario | VLAN 10 / DHCP | `10.21.68.10/25` |
| ISP | WAN hacia FG2 | `21.68.2.1/30` |
| FG2 | WAN | `21.68.2.2/30` |
| FG2 | LAN servidor | `10.21.68.129/28` |
| Servidor Web | HTTPS | `10.21.68.130/28` |

> Ajusta las IP WAN si tu práctica utiliza otras IP públicas. La red LAN
> solicitada queda basada en `10.21.68.x`.

## Configuración

### FortiGate 1

- Interfaces de red.
- VLAN 10.
- DHCP.
- Políticas de firewall.
- NAT.
- VPN IPsec Site-to-Site.

### FortiGate 2

- Interfaces de red.
- Red del servidor.
- Políticas de firewall.
- NAT.
- VPN IPsec Site-to-Site.

### Servidor Web

- Dirección IP: `10.21.68.130/28`
- Gateway: `10.21.68.129`
- Servicio: HTTPS/443

## Validación

### VPN activa

Se verifica que el usuario pueda comunicarse con el servidor mediante:

```bash
ping 10.21.68.130
```

y:

```bash
traceroute 10.21.68.130
```

También se verifica el acceso:

```text
https://10.21.68.130
```

### VPN desactivada

Se deshabilita temporalmente el túnel IPsec y se comprueba que la
comunicación entre el usuario y el servidor deje de funcionar.

### VPN restaurada

Se habilita nuevamente el túnel y se comprueba que la comunicación vuelva
a funcionar.

## Evidencias

Las capturas de la práctica se encuentran en la carpeta `evidencias/`.

## Seguridad

No se deben publicar contraseñas, PSK, claves privadas, certificados privados
ni otros secretos dentro del repositorio.

## Conclusión

La práctica permitió implementar una VPN Site-to-Site entre dos FortiGate y
comprobar la comunicación segura entre una red de usuarios y un servidor HTTPS.
También se validaron VLAN, DHCP, NAT y conectividad mediante ping y traceroute.
