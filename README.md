# ParcheL2Freya

Repositorio publico de parches para el cliente Ascension Lineage II Freya /
High Five. El launcher consulta el Release mas reciente y verifica la firma
ECDSA P-256 del manifiesto antes de instalar cualquier archivo.

## Publicar una version

El PC mantenedor necesita Windows, PowerShell, GitHub CLI autenticado con
permiso para publicar Releases y la clave privada protegida por DPAPI para la
cuenta de Windows que firma los parches. La clave privada no se guarda en este
repositorio ni se incluye en las descargas.

Edita `patch-files.txt` para enumerar rutas relativas autorizadas dentro de la
carpeta del cliente. El publicador solo incluye esas rutas. Revisa el contenido
de la lista antes de publicar; no añadas el cliente completo ni archivos sin
autorizacion de redistribucion.

```powershell
.\Publish-ClientPatch.ps1 `
  -Repository "l2freyah5seven7-source/ParcheL2Freya" `
  -ClientRoot "C:\ruta\al\cliente" `
  -Version "1.0.0.1"
```

El ejemplo produce el Release `v1.0.0.1` con ZIP incrementales, el manifiesto
SHA-256 y su firma. Versiones posteriores deben usar tags unicos, por ejemplo
`1.0.0.2`. GitHub impide que usuarios sin permisos escriban en el repositorio;
las firmas protegen adicionalmente contra manifiestos alterados.

Para corregir un Release existente, revisa primero los archivos, vuelve a
firmar el manifiesto y solicita expresamente el reemplazo con
`-ReplaceExisting`. Esta opcion sobrescribe los activos publicos del tag
indicado.

## Archivos del primer parche

El primer parche contiene unicamente los tres archivos modificados y
autorizados por el mantenedor:

- `system/L2.ini`
- `system/ItemName-e.dat`
- `system/Weapongrp.dat`

No incluye el resto del cliente ni los demas DAT del sistema.
