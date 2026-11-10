# Tema 4 · Enrutamiento OSPF, servicios de red y ACL

Práctica en Cisco Packet Tracer: dos sedes (**Sucursal** y **Gerencia**) unidas por un enlace serial, con servidores FTP, DNS y HTTP (`www.asr.com`).

**Ver la presentación en línea:** https://joseoe.github.io/Presentacion-Martin/

## Contenido

| Archivo | Qué es |
|---|---|
| [`TEMA4.pkt`](TEMA4.pkt) | Laboratorio de Packet Tracer (versión 9.0) |
| [`index.html`](index.html) | Diapositivas (6). Se abren en cualquier navegador, también sin internet |
| [`PRUEBAS.md`](PRUEBAS.md) | Pruebas que hay que hacer en el simulador, paso a paso |

## Cómo se presenta

| Tecla | Acción |
|---|---|
| `→` · `Espacio` · clic | Siguiente |
| `←` | Anterior |
| `N` | Notas del orador y cronómetro |
| `F` | Pantalla completa |
| `R` | Reiniciar el cronómetro |

## Configuraciones solicitadas (6)

1. Ruteo por **OSPF** (proceso 1, área 0).
2. En Sucursal, usuario **cliente** con **privilegio nivel 5** que solo pueda ver la tabla de ruteo.
3. **HTTP y DNS** con la página **www.asr.com**.
4. **FTP** con usuario y contraseña **alumno**, solo con permiso de **List**.
5. **ACL en Gerencia** que permite a PC2 y PC3 llegar al servidor FTP, pero no a la página web.
6. **PC0 y PC1** con acceso libre a FTP y web.

## Direccionamiento

| Equipo / interfaz | Dirección | Gateway |
|---|---|---|
| Sucursal G0/0 | 172.16.10.1/16 | — |
| Sucursal G0/1 | 10.0.0.1/8 | — |
| Sucursal S0/1/0 (DCE, clock 64000) | 200.10.10.1/30 | — |
| Gerencia G0/0 | 192.168.10.1/24 | — |
| Gerencia G0/1 | 10.10.0.1/16 | — |
| Gerencia S0/1/0 | 200.10.10.2/30 | — |
| PC0 / PC1 | 172.16.10.2 / .3 | 172.16.10.1 |
| Servidor FTP | 10.0.0.2 | 10.0.0.1 |
| PC2 / PC3 | 192.168.10.2 / .3 | 192.168.10.1 |
| DNS | 10.10.0.2 | 10.10.0.1 |
| HTTP | 10.10.0.3 | 10.10.0.1 |

Todos los equipos usan como servidor DNS el **10.10.0.2**.

## Equipo

| Diapositiva | Integrante |
|---|---|
| 1 · Portada y 6 · Pruebas | José María Ortiz Escamilla |
| 2 · Topología | Karen Pérez Ortiz |
| 3 · OSPF y privilegios | Gerardo |
| 4 · DNS, HTTP y FTP | Valeria Soto Hernández |
| 5 · ACL y acceso libre | Yael Antonio Chávez Atanasio |
