# Pruebas en el simulador

Hacerlas en este orden durante la presentación.

> Antes de empezar: si un ping falla la primera vez, repítelo (el primer paquete se puede perder mientras se resuelve ARP). Si OSPF aún no tiene vecinos, espera unos segundos o pulsa **Fast Forward Time**.

## 1. Ruteo por OSPF

En **Sucursal** → CLI:

```
show ip ospf neighbor
show ip route ospf
ping 192.168.10.2
```

**Esperado:** vecino `2.2.2.2` en estado `FULL`; rutas marcadas con `O` hacia 192.168.10.0/24 y 10.10.0.0/16; el ping responde.

## 2. Usuario cliente nivel 5

En **Sucursal** → CLI, salir con `exit` y volver a entrar con el usuario **cliente** (pide usuario y contraseña):

```
show privilege
show ip route
configure terminal
```

**Esperado:** `Current privilege level is 5`; `show ip route` funciona; `configure terminal` da `% Invalid input`.

## 3. HTTP y DNS (www.asr.com)

En **PC0** → Command Prompt:

```
nslookup www.asr.com
```

Después **PC0** → Web Browser → `http://www.asr.com`

**Esperado:** `nslookup` responde `10.10.0.3` y el navegador carga la página.

## 4. FTP con usuario alumno (solo List)

En **PC0** → Command Prompt:

```
ftp 10.0.0.2
  Username: alumno
  Password: alumno
dir
get <un archivo que salga en dir>
quit
```

**Esperado:** inicia sesión, `dir` muestra los archivos y `get` es rechazado (solo tiene permiso de listar).

## 5. ACL en Gerencia

En **PC2** (o PC3):

- Command Prompt → `ftp 10.0.0.2` con `alumno` / `alumno` → **entra**.
- Web Browser → `http://www.asr.com` → **Request Timeout** (bloqueado).

En **Gerencia** → CLI:

```
show access-lists
```

**Esperado:** las líneas `deny ... eq www` y `permit ... eq ftp` muestran coincidencias (`matches`).

## 6. PC0 y PC1 con acceso libre

En **PC1**:

- Command Prompt → `ftp 10.0.0.2` con `alumno` / `alumno` → **entra**.
- Web Browser → `http://www.asr.com` → **carga la página**.

## Resumen

| # | Desde | Prueba | Resultado |
|---|---|---|---|
| 1 | Sucursal | `show ip ospf neighbor` · `ping 192.168.10.2` | Vecino FULL · ping exitoso |
| 2 | Sucursal | entrar como `cliente` → `show privilege` | Nivel 5 · ve la tabla, no configura |
| 3 | PC0 | Web → www.asr.com | Carga la página |
| 4 | PC0 | `ftp 10.0.0.2` → `dir` / `get` | dir sí · get denegado |
| 5 | PC2 | FTP y Web | FTP sí · Web bloqueada |
| 6 | PC1 | FTP y Web | Ambos funcionan |
