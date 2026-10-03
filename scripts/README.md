## Scripts

### `web-server-https-setup.sh`

Script de apoyo para reproducir la instalación de Apache2 y habilitar HTTPS
con un certificado autofirmado en `WEB-SV-2168`.

Uso (en el servidor, con permisos de administrador):

```bash
sudo ./web-server-https-setup.sh
```

### `test-vpn-connectivity.sh`

Ejecuta las tres pruebas principales hacia el servidor:

1. ICMP (`ping -c 4 10.21.68.130`)
2. HTTPS (`curl -k -I https://10.21.68.130`)
3. Recorrido (`tracepath 10.21.68.130`)

Uso:

```bash
./test-vpn-connectivity.sh
```

o especificando otra IP:

```bash
./test-vpn-connectivity.sh 10.21.68.130
```

## Comandos de verificación

### Switch

```text
show vlan brief
show interfaces trunk
show interfaces status
```

### ISP

```text
show ip interface brief
show ip route
```

### FortiGate (CLI)

```text
get system interface physical
get router info routing-table all
execute dhcp lease-list
show firewall policy
get vpn ipsec tunnel summary
diagnose vpn ike gateway list
diagnose vpn tunnel list
execute ping 10.21.68.130
execute traceroute 10.21.68.130
```

Para ver si el tráfico realmente pasa por el túnel (en FG1):

```text
diagnose sniffer packet any 'host 10.21.68.130 and icmp' 4
```

### PC de usuario

```bash
ip -br a
ip route
ping -c 4 10.21.68.1
ping -c 4 10.21.68.130
traceroute 10.21.68.130
curl -k -I https://10.21.68.130
```

### Servidor web

```bash
ip -br a
ip route
systemctl status apache2
sudo ss -tlnp | grep :443
sudo apache2ctl -S
openssl s_client -connect localhost:443 </dev/null 2>/dev/null | head -n 15
```

### Orden recomendado para comprobar que todo está bien en la topologia :)

1. Switch: la VLAN 10 existe y el trunk hacia FG1 está activo.
2. Usuario: recibió IP por DHCP y llega a su gateway (`10.21.68.1`).
3. WAN: cada FortiGate hace ping a su lado del ISP.
4. VPN: el túnel aparece **up** en ambos FortiGate.
5. Usuario → servidor: ping, traceroute y `https://10.21.68.130`.
6. Bajar el túnel y confirmar que la comunicación se corta.
7. Levantarlo de nuevo y confirmar que vuelve.

