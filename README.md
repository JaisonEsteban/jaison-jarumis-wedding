# Invitación de boda — Jaison & Jarumis

Este paquete contiene una invitación estática para GitHub Pages, integración con Google Forms/Sheets y un script opcional de notificación por correo.

## Antes de publicar: confirmar

- La página usa **4:30 PM** porque esa hora aparece en los detalles del evento. La imagen original decía 4:00 PM.
- Establezca una nueva fecha límite para RSVP dentro de Google Forms. La fecha anterior, 15 de septiembre de 2026, ya pasó.
- Reemplace el marcador de foto por el archivo original de la pareja.
- Verifique dirección, teléfono, Zelle y Cash App.

## 1. Agregar la foto

1. Cambie el nombre de su foto a `couple-photo.jpg`.
2. Colóquela dentro de la carpeta `assets`.
3. Para mejor resultado, use una imagen horizontal de al menos 1600 × 1200 píxeles.

La página muestra un marcador elegante mientras la foto no exista.

## 2. Crear Google Form

1. Abra https://forms.google.com y seleccione **Formulario en blanco**.
2. Título sugerido: `Confirmación — Boda de Jaison & Jarumis`.
3. Cree la pregunta **¿Asistirás?** como opción múltiple y márquela obligatoria.
4. Opciones: `Sí` y `No`.
5. Cree una sección llamada **Información de los invitados que asistirán**.
6. Dentro de esa sección agregue:
   - `Nombre completo` — respuesta corta, obligatoria.
   - `Número de teléfono` — respuesta corta, opcional.
   - Cualquier otra información que realmente necesite.
7. En la pregunta **¿Asistirás?**, abra el menú de tres puntos y elija **Ir a la sección según la respuesta**.
8. Configure `Sí` para ir a la sección de información.
9. Configure `No` para **Enviar formulario**.
10. En Configuración → Presentación, escriba un mensaje de confirmación como: `Gracias por responder. Hemos recibido tu confirmación.`

## 3. Conectar Google Sheets

1. Abra el formulario.
2. Entre a **Respuestas**.
3. Seleccione el icono verde de Google Sheets.
4. Elija **Crear una hoja de cálculo nueva**.
5. Cada RSVP aparecerá automáticamente en esa hoja con fecha y hora.

### Resumen opcional en la hoja

Si la respuesta a **¿Asistirás?** queda en la columna B, puede usar:

```text
=COUNTIF(B:B,"Sí")
=COUNTIF(B:B,"No")
```

Cambie `B:B` si la respuesta está en otra columna.

## 4. Insertar Google Form en la invitación

1. En Google Forms seleccione **Enviar**.
2. Seleccione el icono `<>` para insertar HTML.
3. Copie solamente la URL que aparece dentro de `src="..."`.
4. Abra `index.html`.
5. Busque `PASTE_GOOGLE_FORM_EMBED_URL_HERE`.
6. Reemplácelo por la URL copiada, conservando las comillas.

Ejemplo:

```javascript
const GOOGLE_FORM_EMBED_URL = "https://docs.google.com/forms/d/e/FORM_ID/viewform?embedded=true";
```

## 5. Activar notificaciones por correo (opcional)

Google Forms ya guarda todas las respuestas sin este paso. Use el script solamente si desea recibir un correo con cada RSVP.

1. Abra la hoja de Google Sheets conectada al formulario.
2. Seleccione **Extensiones → Apps Script**.
3. Borre el contenido inicial y pegue `google-apps-script.gs`.
4. Cambie `REPLACE_WITH_YOUR_EMAIL@example.com` por el correo que recibirá las alertas.
5. Guarde el proyecto.
6. Seleccione **Activadores** en la barra izquierda.
7. Agregue un activador para `onFormSubmit`.
8. Fuente del evento: **Desde la hoja de cálculo**.
9. Tipo de evento: **Al enviar el formulario**.
10. Autorice el acceso solicitado por Google.

## 6. Probar localmente

La forma más sencilla es abrir `index.html` en Safari o Chrome.

Pruebe lo siguiente:

- Foto o marcador visible.
- Cuenta regresiva funcionando.
- Botón **Cómo llegar** abre Google Maps.
- Botón del teléfono funciona en un móvil.
- Formulario carga y acepta una respuesta de prueba.
- La respuesta aparece en Google Sheets.
- El correo de notificación llega, si activó el script.

## 7. Publicar gratis con GitHub Pages

1. Inicie sesión en https://github.com.
2. Cree un repositorio nuevo, por ejemplo `wedding-invitation`.
3. Un repositorio público funciona con GitHub Pages en el plan gratuito. Recuerde que el código será visible públicamente.
4. Seleccione **Add file → Upload files**.
5. Suba:
   - `index.html`
   - la carpeta `assets` con `couple-photo.jpg`
6. Confirme la carga con **Commit changes**.
7. Abra **Settings → Pages**.
8. En **Build and deployment**, seleccione **Deploy from a branch**.
9. Seleccione la rama `main` y la carpeta `/ (root)`.
10. Presione **Save**.
11. GitHub mostrará una dirección parecida a `https://usuario.github.io/wedding-invitation/`.

No suba `google-apps-script.gs` si no desea que el script y el correo configurado sean visibles en el repositorio público. Ese archivo solamente debe pegarse en Google Apps Script.

## 8. Actualizar la invitación

Para cambiar texto, enlaces o la foto, cargue el archivo actualizado en el mismo repositorio y confirme los cambios. GitHub Pages publicará la actualización automáticamente.

## Privacidad

- La página solicita a los buscadores que no la indexen, pero eso no equivale a una contraseña.
- Cualquier persona con el enlace puede ver la dirección y los datos mostrados.
- No coloque contraseñas, credenciales de Google, claves API ni información bancaria sensible dentro del HTML.
- Cuando termine la boda, puede desactivar GitHub Pages, archivar las respuestas y eliminar el formulario.
