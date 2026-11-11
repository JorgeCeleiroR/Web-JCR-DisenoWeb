# Comprobaciones con DevTools

Capturas hechas con las herramientas de desarrollo del navegador sobre elementos de SurfAlquila.

## 1. Regla sobrescrita (cascada)

![Cascada en el botón Ver catálogo](capturas/01-cascada.png)

**Elemento inspeccionado:** el botón «Ver catálogo» de `index.html` (`<a class="boton">`).

**Qué he comprobado:** en el panel Styles aparecen dos reglas que dan color al texto del enlace:
- `h1, h2, h3, a { color: #0b3d91; }` (`estilos.css`, línea 9): aparece **tachada**, no se aplica.
- `.boton { color: white; }` (`estilos.css`, línea 54): es la que **se aplica**.

**Valor final:** texto blanco (`white`) sobre fondo `#0b3d91`.

**Por qué:** las dos reglas afectan al mismo elemento y a la misma propiedad. Gana `.boton` porque un selector de clase tiene más especificidad que un selector de tipo (`a`). La hoja de estilos del navegador (`a:-webkit-any-link`) también aparece tachada, porque nuestras reglas tienen prioridad sobre ella.

Sin la regla `.boton`, el texto del botón se vería azul sobre fondo azul y no se podría leer.

## 2. Modelo de caja

![Modelo de caja de una tarjeta](capturas/02-modelo-caja.png)

**Elemento inspeccionado:** una tarjeta del catálogo (`<article class="tarjeta">`), pestaña Computed.

**Valores observados:**
| Zona | Valor |
|---|---|
| Margen | 0 |
| Borde | 2 px, sólido, `rgb(11, 61, 145)` (`#0b3d91`) |
| Relleno | 16 px por cada lado |
| Contenido | 270,656 × 602,328 px |

**Qué he comprobado:** que los valores coinciden con el CSS de `.tarjeta` (`border: 2px solid #0b3d91; padding: 16px;`) y que no tiene margen, porque la separación entre tarjetas la da el `gap` del grid.

**Medida total:** como la hoja usa `box-sizing: border-box` para todos los elementos, el ancho que se ve en pantalla es 270,656 + 16 + 16 + 2 + 2 = **306,656 px**.

**Altura:** el alto del contenido (602,328 px) no es fijo; se adapta al contenido de la tarjeta (imagen, texto y precio).

