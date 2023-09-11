---
title: Cómo convertir códigos de demostración para que estén "en vivo"
slug: MDN/Writing_guidelines/Page_structures/Live_samples
---

{{MDNSidebar}}

MDN tiene ahora un sistema de "ejemplos en vivo", donde el código de demostración que aparece en la página se usa directamente para mostrar el resultado de dicho ejemplo. Sin embargo, muchos artículos existentes tienen ejemplos que todavía no usan este sistema y necesitan ser convertidos.

<table>
  <tbody>
    <tr>
      <td><strong>¿Dónde hay que hacerlo?</strong></td>
      <td>
        En artículos etiquetados como
        <a href="/es/docs/tag/NeedsLiveSample">NecesitaMuestraEnVivo</a
        > (<a href="/es/docs/tag/NeedsLiveSample">NeedsLiveSample</a>)
      </td>
    </tr>
    <tr>
      <td><strong>¿Qué necesitas saber para hacer esta tarea?</strong></td>
      <td>
        <ul>
          <li>
            Entender HTML, CSS y/o JavaScript, dependiendo del código de muestra
            que sea.
          </li>
          <li>
            Habilidad para usar macros
            <a
              href="https://developer.mozilla.org/es/docs/Project:MDN/Kuma/Introduction_to_KumaScript"
              >KumaScript</a
            >
            dentro de los artículos MDN.
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><strong>¿Cuáles son los pasos para hacer la tarea?</strong></td>
      <td>
        <p>
          Para una descripción completa del sistema de demostración en vivo,
          incluyendo cómo crear las demostraciones en vivo, ver
          <a
            href="/es/docs/Project:MDN/Contributing/Editor_guide/Live_samples"
            >Usar el sistema de demostración en vivo</a
          >.
        </p>
        <ol>
          <li>
            Elige un artículo de la lista de artículos etiquetados como
            <a
              style="text-decoration: underline"
              href="/es/docs/tag/NeedsLiveSample"
              >NecesitaMuestraEnVivo</a
            >
            (<a href="/es/docs/tag/NeedsLiveSample">NeedsLiveSample</a>),
            donde el código sea para una característica con la que sientas que
            estas familiarizado.
          </li>
          <li>Convierte el código para que sea "en vivo".</li>
          <li>
            Borra cualquier código o imagen que haya sido usada para mostrar el
            resultado de la demostración.
          </li>
        </ol>
        <p></p>
      </td>
    </tr>
  </tbody>
</table>
