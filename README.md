# Ethos v5.0

Archivos:
- `index.html` → la web completa (súbela donde la tengas alojada, sustituyendo la anterior).
- `firestore.rules` → reglas de seguridad para pegar en Firebase.

## Lo que tienes que hacer (una sola vez, ~5 min)

### 1. Activar el login en Firebase
1. Entra en https://console.firebase.google.com → proyecto **ethosgames-a1bc1**.
2. **Build → Authentication → Get started → Sign-in method** → activa **Correo electrónico/contraseña**.
3. Pestaña **Users → Add user**: email `ericaguera02@gmail.com` + la contraseña que quieras.
   (Hazlo ya, antes de publicar la web: así nadie más puede registrar ese email.)
4. **Authentication → Settings → Authorized domains**: comprueba que el dominio donde alojas Ethos está en la lista (añádelo si no).

### 2. Publicar las reglas de Firestore (lo que realmente protege tu base de datos)
1. **Build → Firestore Database → Rules**.
2. Borra lo que haya, pega el contenido de `firestore.rules` y pulsa **Publish**.
   - Si tenías algo como `allow read, write: if true;`, ese era el agujero: cualquiera podía borrar o cambiar tus juegos.

### 3. Subir `index.html`
Sustituye el archivo anterior en tu hosting. Entra en `#/admin` con tu email y la contraseña del paso 1.

## Funciones nuevas
- **Música Ousify**: botón ♪ (o tecla `M`). Panel flotante que sigue sonando mientras navegas o juegas; `—` minimiza, `↗` lo saca a ventana aparte, `✕` lo cierra y para.
- **Radio por categoría**: al abrir un juego o elegir una categoría, el panel sugiere una búsqueda (acción → "epic action music", etc.). Botón "Poner radio" o casilla **Auto**. Edita la lista `RADIO` en el código para cambiar los géneros.
- **Juegos que no cargan**: en Admin, botón **Marcar ↗** (o la casilla al editar). Esos juegos se abren directamente en pestaña nueva. Dentro del reproductor, como admin, verás **🚫 No carga** para marcarlos al momento.
- **Colores**: botón 🎨 en la barra (7 temas, se recuerda).
- **Intro**: animación de entrada (una vez por sesión; clic o tecla para saltarla).
- **Salida rápida**: `Esc` dos veces, la tecla ` o el botón 📄 te llevan a Google Docs (`PANIC_URL` en el código). Si el foco está dentro del juego, el navegador no pasa las teclas a Ethos: usa el botón 📄.

## Ousify dentro de Ethos
Un iframe solo funciona si Ousify lo permite. Si el panel sale en blanco o con error, en el proyecto de Ousify (Vercel) añade un `vercel.json`:

```json
{
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        { "key": "Content-Security-Policy", "value": "frame-ancestors 'self' https://TU-DOMINIO-DE-ETHOS" }
      ]
    }
  ]
}
```
y quita cualquier `X-Frame-Options: DENY`. Mientras tanto, el botón `↗` abre Ousify en ventana aparte.

La radio usa `https://ousify-main.vercel.app/?q=<búsqueda>`. Si Ousify aún no lee el parámetro `q`, abrirá su inicio normal; hay que añadirlo en Ousify para que busque solo.

## Nota
La `apiKey` de Firebase en el HTML es pública por diseño; la seguridad la dan las reglas del paso 2.
