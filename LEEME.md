# Fotos de sensores en obra — Nivel 02

Página para que el técnico tome la foto de cada sensor de detección de incendios
tocando su círculo en el croquis. Las fotos se guardan en tu Google Drive.

```
sensores-obra/
├── index.html        la página (no hace falta tocarla)
├── config.js         aquí pegas la URL de Google y la clave
├── plano.png         el croquis del DWG convertido a imagen
└── apps-script/
    └── Code.gs       el script que guarda las fotos en tu Drive
```

Son tres partes. Hazlas en este orden.

---

## Parte 1 — El script de Google (donde se guardan las fotos)

1. Entra a <https://script.google.com> con tu cuenta de Gmail y da clic en **Nuevo proyecto**.
2. Ponle nombre arriba a la izquierda, por ejemplo `Fotos sensores`.
3. Borra todo lo que trae el editor y pega el contenido de `apps-script/Code.gs`.
4. En la línea `const CLAVE = 'cambia-esta-clave';` cambia el texto por una clave tuya,
   por ejemplo `nivel02-2026`. Anótala, la vas a usar en la Parte 2.
5. Guarda (ícono de disquete o Ctrl+S).
6. Arriba, en la lista de funciones, elige **prueba** y da clic en **Ejecutar**.
   Google te pedirá permisos: **Revisar permisos → tu cuenta → Configuración avanzada →
   Ir a Fotos sensores (no seguro) → Permitir**. Es normal que diga "no seguro" porque el
   script es tuyo y no lo ha revisado Google.
   Al terminar se crea en tu Drive la carpeta **Fotos sensores - Nivel 02**.
7. Da clic en **Implementar → Nueva implementación**.
   - En el engrane de "Seleccionar tipo" elige **Aplicación web**.
   - **Ejecutar como:** Yo (tu correo).
   - **Quién tiene acceso:** Cualquier usuario.
   - Da clic en **Implementar** y copia la **URL de la aplicación web** (termina en `/exec`).

> Si después cambias algo en `Code.gs`, usa **Implementar → Gestionar implementaciones →
> editar (lápiz) → Versión: Nueva versión**. Así la URL no cambia.

## Parte 2 — Configurar la página

Abre `config.js` y llena:

```js
API_URL: 'https://script.google.com/macros/s/XXXXXXXX/exec',  // la URL del paso 7
CLAVE: 'nivel02-2026',                                         // la misma del paso 4
OBRA: 'Nivel 02'
```

## Parte 3 — Subirlo a GitHub Pages

1. En GitHub crea un repositorio nuevo, por ejemplo `sensores-obra`. Puede ser público.
2. Da clic en **Add file → Upload files** y arrastra `index.html`, `config.js`, `plano.png`
   y `LEEME.md`. (La carpeta `apps-script` no hace falta subirla, pero no pasa nada si la subes.)
3. Da clic en **Commit changes**.
4. Ve a **Settings → Pages**. En **Source** elige **Deploy from a branch**, rama **main**,
   carpeta **/ (root)** y da clic en **Save**.
5. En uno o dos minutos aparece arriba la dirección:
   `https://TU-USUARIO.github.io/sensores-obra/`

Esa dirección es la que le mandas al técnico por WhatsApp. No necesita cuenta ni contraseña.

---

## Antes de mandarlo a campo

Abre la dirección en tu teléfono, toca un sensor, toma una foto y revisa:
- que el círculo se ponga verde,
- que la foto aparezca en tu carpeta **Fotos sensores - Nivel 02** de Drive,
- que en la foto se vea la franja con la etiqueta y el recorte del plano.

Para borrar una foto equivocada, bórrala en la carpeta de Drive. En menos de un minuto
el sensor vuelve a amarillo en la página.

## Cómo quedan las fotos

En la carpeta de Drive cada archivo se llama así:

```
SH-014__20261030-131245__a1b2.jpg
```

Etiqueta del sensor, fecha y hora, y un código corto. Al ordenar por nombre quedan agrupadas
por sensor. Para bajarlas todas: clic derecho en la carpeta → **Descargar** (Drive te da un ZIP).

## Si algo no funciona

| Lo que ves en la página | Qué hacer |
|---|---|
| "Falta configurar…" | `API_URL` está vacío en `config.js`. |
| "La clave de config.js no coincide…" | La clave de `config.js` y la de `Code.gs` deben ser idénticas. |
| "No se pudo conectar con Google Drive" | Revisa que la implementación diga **Cualquier usuario** y que la URL termine en `/exec`. |
| "No se pudo subir la foto" | Casi siempre es la señal. El técnico puede tocar **Reintentar** o **Guardar en el teléfono** y mandártela. |
| Las miniaturas no cargan | Espera un minuto; Drive tarda un poco en generar la vista previa. |

## Sobre la privacidad

- La página es pública, pero sin la clave nadie puede ver la lista de fotos ni subir nada.
  Como la clave viaja dentro de `config.js`, alguien que revise el código de la página
  podría verla. Para una obra suele ser suficiente; no la uses en algo confidencial.
- Las fotos quedan compartidas "cualquiera con el enlace" para que la página muestre las
  miniaturas. Nadie las encuentra si no tiene el enlace exacto de cada una.

## Sensores

El plano tiene 67 sensores: 62 de humo (SH-001 a SH-061, más el SH-001 repetido) y 5 de calor (SC-001 a SC-005).
En el DWG hay **dos sensores con la etiqueta SH-001**; el segundo aparece como `SH-001 (2)`.
Para corregirlo, en `index.html` busca `"SH-001-B","SH-001 (2)"` y cambia ambos textos por la
etiqueta correcta, por ejemplo `"SH-062","SH-062"`.
