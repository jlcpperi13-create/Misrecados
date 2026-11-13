# MisRecados

Compras y recados de la familia en una sola lista compartida. Cada encargo lleva el nombre de quien lo pide.

## Archivos
- `index.html` — la app completa
- `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png` — para instalarla como PWA
- `firestore.rules` — reglas de seguridad (copiar en Firebase)

## Puesta en marcha (≈15 min)

1. **Firebase → Crear proyecto** (por ejemplo `misrecados`).
2. **Authentication → Sign-in method**: activa **Google** y **Correo/contraseña**.
3. **Firestore Database → Crear base de datos** (modo producción, región `europe-west`).
4. **Firestore → Reglas**: borra lo que hay, pega el contenido de `firestore.rules` y pulsa **Publicar**.
5. **Configuración del proyecto → Tus apps → Web (</>)**: registra la app y copia el objeto `firebaseConfig` dentro de `index.html`, donde pone `PEGA_AQUI`.
6. Sube los archivos a un repositorio de GitHub y activa **GitHub Pages**.
7. **Authentication → Configuración → Dominios autorizados**: añade `TUUSUARIO.github.io`.
8. Abre la web en Chrome → menú ⋮ → **Instalar app**.

## Cómo se usa
- El primero crea la familia y comparte el **código de 6 letras** (botón 👪 Familia → Compartir).
- Los demás entran, ponen su nombre y se unen con el código.
- **+** para apuntar algo: qué, dónde y urgencia.
- **🙋 Me lo llevo yo** → nadie más lo compra por duplicado.
- **✅ Entregado** → a quien lo pidió le llega un aviso.

## Estructura de datos
```
usuarios/{uid}            nombre, familiaId
codigos/{CODIGO}          familiaId, creadoPor
familias/{fid}            nombre, codigo, miembros[], miembrosInfo{uid:{nombre,color}}
familias/{fid}/items/{id} que, detalle, donde, urgencia, estado,
                          pedidoPor, pedidoPorNombre, encargadoPor, encargadoPorNombre,
                          creado, encargadoEn, entregadoEn
```
Estados: `pendiente` → `encargado` → `entregado`.
