---
title: "Antigravity IDE desde la terminal: crea un comando CLI como 'code .' en PowerShell"
author: "Ing. Jesús Antonio Chávez Becerra"
role: "Arquitecto de Soluciones | Arquitecto DevSecOps"
date: 2026-07-23
---

<p align="center">
  <img src="https://antigravity.google/assets/image/brand/antigravity_product_lockup_full_color_reverse.png" alt="Antigravity IDE Logo" width="120"/>
</p>

# Antigravity IDE — Cómo abrirlo desde cualquier carpeta en PowerShell

> **Aprende a crear un comando `antigravity` para abrir el IDE directamente desde la terminal, tal como lo haces con `code .` en Visual Studio Code.**

---

## Introducción

Si trabajas con **Antigravity IDE** y estás acostumbrado a la productividad que te da escribir `code .` para abrir Visual Studio Code en el directorio actual, te alegrará saber que puedes lograr exactamente lo mismo con Antigravity IDE.

En esta guía te mostraré paso a paso cómo configurar PowerShell para que el comando `antigravity .` abra tu IDE favorito apuntando a la carpeta donde te encuentres.

---

## Requisito previo

Antigravity IDE debe estar instalado en tu sistema. Por defecto se instala en la siguiente ruta:

```
$env:LOCALAPPDATA\Programs\Antigravity IDE\Antigravity IDE.exe
```

Que en la mayoría de los casos resuelve a:

```
C:\Users\<tu-usuario>\AppData\Local\Programs\Antigravity IDE\Antigravity IDE.exe
```

> **Importante:** Antes de continuar, verifica que la ruta del ejecutable coincida en tu PC. Abre PowerShell y ejecuta:
>
> ```powershell
> Test-Path "$env:LOCALAPPDATA\Programs\Antigravity IDE\Antigravity IDE.exe"
> ```
>
> Debe devolver `True`. Si el ejecutable está en otra ubicación, ajusta la ruta en los pasos siguientes.

---

## Paso 1: Abrir el perfil de PowerShell

El perfil de PowerShell (`$PROFILE`) es un script que se ejecuta automáticamente cada vez que inicias una nueva sesión. Aquí agregaremos nuestra función personalizada.

```powershell
notepad $PROFILE
```

Si el archivo no existe, PowerShell lo creará automáticamente al guardar.

---

## Paso 2: Agregar la función

Copia y pega el siguiente bloque al final del archivo:

```powershell
function antigravity {
    param([string]$Path = ".")
    & "$env:LOCALAPPDATA\Programs\Antigravity IDE\Antigravity IDE.exe" $Path
}
```

**Explicación:**

| Elemento | Descripción |
|---|---|
| `function antigravity` | Define un comando personalizado llamado `antigravity` |
| `param([string]$Path = ".")` | Acepta una ruta como argumento; por defecto usa el directorio actual (`.`) |
| `$env:LOCALAPPDATA` | Variable de entorno que se adapta automáticamente al usuario actual |
| `& "..." $Path` | Ejecuta el ejecutable del IDE pasándole la ruta recibida |

Guarda y cierra el archivo.

---

## Paso 3: Recargar el perfil

Para que los cambios surtan efecto **de forma inmediata** en la sesión actual:

```powershell
. $PROFILE
```

O bien **cierra y abre una nueva terminal de PowerShell**. Es necesario hacer esto para que la función esté disponible.

---

## Modo de uso

Una vez configurado, puedes usar el comando de las siguientes maneras:

| Comando | Resultado |
|---|---|
| `antigravity .` | Abre el IDE en el directorio actual |
| `antigravity` | Abre el IDE en el directorio actual (por defecto) |
| `antigravity C:\ruta\proyecto` | Abre el IDE en la ruta especificada |
| `antigravity ..` | Abre el IDE en el directorio padre |

### Ejemplo práctico

```powershell
PS C:\Users\usuario\proyectos\mi-app> antigravity .
```

Esto lanzará Antigravity IDE con el proyecto `mi-app` cargado automáticamente.

---

## Notas importantes

- El comando ejecuta el `.exe` directamente (modo GUI), no el `cli.js` del IDE.
- La función usa `$env:LOCALAPPDATA` para que sea **portable entre distintos usuarios de Windows** sin necesidad de modificar la ruta manualmente.
- Si cambias la ruta de instalación de Antigravity IDE, solo debes actualizar la línea dentro de la función en `$PROFILE`.
- Si prefieres un nombre de comando más corto, puedes renombrar la función de `antigravity` a `ag` o el alias que prefieras.

---

## Conclusión

Con esta sencilla configuración, ahora puedes abrir Antigravity IDE desde cualquier ubicación de tu terminal con un solo comando. Pequeños ajustes como este mejoran significativamente el flujo de trabajo diario, especialmente cuando trabajas con múltiples proyectos y terminales.

---

<p align="center">
  <strong>Ing. Jesús Antonio Chávez Becerra</strong><br>
  Arquitecto de Soluciones & Arquitecto DevSecOps<br>
  <br>
  🌐 <a href="https://devsecops.pe">devsecops.pe</a><br>
  ✉️ <a href="mailto:jesus@devsecops.pe">jesus@devsecops.pe</a>
</p>

---

<p align="center" style="color: #888; font-size: 0.9em;">
  © 2026 Jesús Antonio Chávez Becerra — Todos los derechos reservados.
</p>
