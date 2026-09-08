# Guía de Mantenimiento y Automatización del Perfil de GitHub

## Parte 1: Añadir recursos visuales locales (Ej. Títulos con efectos / SVGs)
Para evitar depender de servicios externos de imágenes que puedan fallar, los recursos gráficos personalizados se alojan directamente en el repositorio.

1. **Crear la estructura:** Crea una carpeta en la raíz de tu repositorio llamada `assets/`.
2. **Añadir el archivo:** Dentro de `assets/`, coloca tu archivo gráfico (por ejemplo, `glow-title.svg`). 
   * *Nota:* Este archivo contendrá el diseño visual, los efectos de brillo y el texto exacto que se mostrará en pantalla.
3. **Vincularlo en el README:** En tu archivo `README.md` principal, elimina cualquier referencia a imágenes externas y apunta de forma local mediante una etiqueta HTML centrada:
   
   ```html
   <div align="center">
     <img src="./assets/glow-title.svg" alt="Descripción de tu título">
   </div>

---

## Parte 2: Automatización de Estadísticas con GitHub Actions (Cero Dependencias Externas)

Para generar tarjetas de estadísticas, lenguajes y rachas de forma local y automática sin tirar de servidores de terceros inestables:

* **Estructura de directorios:** Crea una carpeta oculta `.github/` y dentro otra llamada `workflows/` (es decir, `.github/workflows/`).
* **Organización de archivos:** Es mucho mejor mantener los archivos de workflows separados según su propósito (por ejemplo, un `stats.yml` para las tarjetas del perfil) para que el código sea limpio y fácil de depurar si falla algo.
* **Creación del archivo YAML:** Dentro de `.github/workflows/`, crea el archivo `stats.yml` con la estructura de automatización necesaria.
* **Personalización manual de colores:** Dentro de las opciones del archivo de configuración, puedes definir manualmente los colores de los iconos y elementos mediante parámetros hexadecimales (por ejemplo, añadiendo `&icon_color=FFA500` para un tono naranja armónico).

---

## Parte 3: Ejecución, Generación y Limpieza de Caché

Una vez configurado todo el entorno, el flujo para aplicar y actualizar los gráficos es el siguiente:

* **Ejecutar la Action:**
  1. Ve a la pestaña **Actions** en la interfaz web de tu repositorio de GitHub.
  2. Selecciona el workflow correspondiente en la barra lateral (ej. *Update README cards*).
  3. Haz clic arriba a la derecha en **Run workflow** y confirma la ejecución. (Si no lo ejecutas manualmente, se ejecuta igual cada medianoche automáticamente) 
* **Verificación de archivos generados:**
  1. Cuando el proceso termine con éxito (marcado en verde), la propia acción creará automáticamente una carpeta llamada `profile/` en tu repositorio.
  2. Dentro de esa carpeta encontrarás los archivos SVG compilados localmente, como por ejemplo: (`stats.svg`, `top-langs.svg` y `streak.svg`).
* **Conectar el README:**
  Asegúrate de que tu `README.md` principal no apunte a enlaces web externos, sino directamente a los archivos locales generados utilizando la ruta correspondiente.
* **Solución a problemas de visualización o caché:**
  1. Si tras actualizar los colores o ejecutar el workflow notas que el perfil sigue mostrando los diseños antiguos, entra de manera individual a los archivos dentro de la carpeta `profile/` en la pestaña de código para confirmar que se han actualizado.
  2. En tu perfil principal osea al estar dentro de `stats.svg` u otro, presiona **Ctrl + F5** (o limpia la caché del navegador) para forzar la recarga visual. Si persiste, vuelve a lanzar el *Run workflow* previo y repite el refresco. Todo quedará sincronizado correctamente.
