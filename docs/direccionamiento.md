# Direccionamiento IP

## Red de usuarios

- Red: `10.21.68.0/25`
- Gateway: `10.21.68.1`
- DHCP: según el rango configurado en FortiGate
- VLAN: `10`

## Red del servidor

- Red: `10.21.68.128/28`
- Gateway: `10.21.68.129`
- Servidor: `10.21.68.130`

## VPN IPsec

- Red local FG1: `10.21.68.0/25`
- Red remota FG1: `10.21.68.128/28`

En FG2 los selectores se invierten:

- Red local FG2: `10.21.68.128/28`
- Red remota FG2: `10.21.68.0/25`
