# Informe – Práctica P1

**Estudiante:** Diomedes Mateo Alvarez
**Matrícula:** 20250873
**Video de demostración:** https://youtu.be/CzorAFQLSbI

## 1. Objetivo

Diseñar e implementar en GNS3 una topología que integre un proveedor de
servicio (ISP), un firewall FortiGate, un router de sucursal y las redes
internas de las áreas ADMIN, USER, DB y WEB, verificando su conectividad.

## 2. Topología

![Topología](topologia.png)

### 2.1 Componentes

| Nodo | Dispositivo | IP planeada | Descripción |
|------|-------------|-------------|-------------|
| NAT1 | Cloud (NAT) | – | Salida a Internet |
| ISP | Cisco IOSvL2 | 203.0.113.1 | Enrutamiento del proveedor |
| FortiGate-6.4.6-1 | FortiGate 6.4.6 | 192.168.10.1 (LAN) | Firewall y segmentación |
| Switch1 | Ethernet switch | – | Medio de acceso de las áreas |
| BRANCH | Cisco IOSvL2 | 10.0.0.1 | Router de sucursal |
| ADMIN | VPCS | 192.168.10.10 | Estación de administración |
| USER | VPCS | 192.168.10.20 | Estación de usuarios |
| DB | VPCS | 192.168.10.30 | Servidor de base de datos |
| WEB | VPCS | 10.0.0.20 | Servidor web de sucursal |

> Ajusta las direcciones IP a las usadas en tu laboratorio antes de entregar.

## 3. Descripción de la implementación

1. **NAT1 – ISP:** enlace de salida hacia Internet mediante la nube NAT.
2. **ISP – FortiGate / ISP – BRANCH:** enlaces punto a punto de la zona
   perimetral.
3. **FortiGate – Switch1:** el firewall actúa como puerta de enlace de las
   áreas ADMIN, USER y DB.
4. **BRANCH – WEB:** enlace del router de sucursal hacia el servidor web.

## 4. Configuraciones

Las configuraciones de cada dispositivo se encuentran en la carpeta `configs/`
y la de las PCs en `hosts/vpcs_hosts.cfg`.

## 5. Verificación de conectividad

Ejecutar `scripts/verificar_conectividad.bat` o los `ping` manualmente desde
VPCS:

- ADMIN → DB
- USER → DB
- ADMIN/USER → WEB (a través del FortiGate y BRANCH)
- WEB → NAT1 (salida a Internet)

## 6. Conclusiones

_Escribe aquí tus conclusiones._
