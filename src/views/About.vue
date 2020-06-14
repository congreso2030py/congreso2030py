<template>
  <div>
    <div id="about" class="o-container o-section u-margin-bottom-10">
      <tipi-header title="Acerca"/>
        <div class="o-grid">
          <div class="o-grid__col u-8@sm u-offset-2@sm">

            <tipi-message icon type="info">
              La <strong>versión beta</strong> incluye:
              <br>
              <ul>
                <li>Datos...</li>
                <li>Funcionalidades</li>
                <li>Duración...</li>
              </ul>
            </tipi-message>

            <p><strong>Congreso2030py</strong> es una innovadora herramienta que rastrea, reúne y ofrece la información sobre la actividad del Congreso Nacional de la República del Paraguay relacionada con los Objetivos de Desarrollo Sostenible. Fue diseñada para superar los retos que plantea la naturaleza transversal de la Agenda 2030, Congreso 2030Py clasifica la información relacionada con los ODS gracias a un avanzado sistema automático de etiquetado masivo. Esta innovadora tecnología permite a los usuarios navegar por la actividad parlamentaria relacionada con los ODS a través de un buscador online, abierto y gratuito. La información ofrecida es esencial de cara a la monitorización y la rendición de cuentas de la implementación de la Agenda 2030 a nivel nacional.</p>
            <h4>¿Cómo funciona?</h4>
            <p>Congreso 2030Py reúne toda la información publicada por el Congreso Nacional de la República del Paraguay, a través del SILPY, y crea una base de datos a través de un proceso automático de etiquetado masivo que la clasifica de acuerdo a su relación con cualquier ODS o meta. Combina ciencia informática avanzada - necesaria para escrapear miles de PDFs en los que se publica la información parlamentaria y transformarlos en una base de datos estructurada - con el diseño de unos diccionarios de ODS que automáticamente relacionan iniciativas políticas con objetivos y las metas. Después, a través de un buscador intuitivo, atractivo y accesible, ofrece toda la información relevante en formatos reutilizables. Los usuarios pueden seleccionar sus propios términos en el buscador para adaptar las búsquedas a sus necesidades.</p>
            <h4>¿Qué respuestas ofrece?</h4>
            <p>Congreso 2030Py ayuda a encontrar las respuestas menos obvias a complicadas preguntas a primera vista: ¿Qué ODS se ven afectados por determinadas iniciativas legislativas? ¿Cuáles objetivos o metas reciben una mayor atención de los diputados y senadores y cuáles son los grandes olvidados? ¿Quiénes son los diputados y senadores más activos en la implementación de la Agenda 2030 y quiénes aportan menos al debate? Además, ofrece un método de gran eficiencia para analizar la actividad política al permitir detectar toda la actividad legislativa relacionada con un determinado ODS o meta propuesta y debatida al mismo tiempo en los diferentes ámbitos del Congreso.</p>
            <h4>¿Por qué el Congreso?</h4>
            <p>Los parlamentos nacionales tienen una posición clave en el proceso de implementación de la Agenda 2030. Son la institución pública más relevante y mejor posicionada para asegurar la coherencia con el desarrollo sostenible en los cientos de miles de leyes, iniciativas legislativas, planes públicos y presupuestos que se aprobarán en cada país en los próximos años.</p>
            <h4>¿Es adaptable a otros países?</h4>
            <p>Sí, su adaptación es posible. En el caso del Congreso Nacional paraguayo, la implementación se realizó gracias al interés inicial de la Cámara de Senadores de adaptarla como parte de su plan de transparencia y de apertura legislativa, su implementación contó con el apoyo y la financiación de EUROsociAL+ y FIIAPP a través del Área de Políticas de Gobernanza Democrática.</p>
            <p>La tecnología fue inicialmente adaptada e implementada en el Congreso de los Diputados de España a través de la herramienta <a href="https://parlamento2030.es" target="_blank">Parlamento 2030</a>, debido al interés del gobierno español de incluir la herramienta como parte de su Plan de Acción para la Implementación de la Agenda 2030, presentado ante Naciones Unidas en 2018.</p>
            <p>Al igual que ha sido adaptado a los parlamentos español y paraguayo es posible hacerlo a los parlamentos de otros países o a otros niveles de la administración pública. Ya sea otro país, una región o el Parlamento Europeo o quienes muestren interés, esta tecnología puede ser rápidamente adaptada en un corto periodo de tiempo a cualquiera de estos marcos debido al código abierto utilizado.</p>
            <h4>¿Quiénes somos?</h4>
            <p>Congreso2030py y su versión española Parlamento 2030 son proyectos diseñados por <a href="http://politicalwatch.es" target="_blank">Political Watch</a>, plataforma que se inscribe dentro de la estrategia del think tank CIECODE y que está formado por profesionales de distintas disciplinas como informáticos, periodistas y economistas. Nuestra misión es fomentar un debate público informado y basado en hechos sobre el desarrollo sostenible. Desarrollamos tecnologías innovadoras que automáticamente rastrean actividad relacionada con el desarrollo sostenible y que ofrecen acceso a esta información de forma pública, directa y gratuita a actores clave y ciudadanos trabajando de la mano con administraciones y organizaciones de la sociedad civil para promover la transparencia y el acceso a la información.</p>
            <p>En el caso de Congreso2030Py, la Cámara de Senadores cuenta con un equipo interdisciplinario de profesionales que se encargan del permanente monitoreo y actualización de la información que arroja la plataforma. Para la revisión y adaptación local de los términos utilizados por la plataforma se cuenta con el apoyo de instituciones del Poder Ejecutivo, la Comisión Nacional de ODS y de organizaciones de la sociedad civil.</p>
          </div>
        </div>
    </div>
  </div>
</template>

<script>

  import { TipiHeader, TipiMessage } from 'tipi-uikit';

export default {
  name: 'about',
  components: {
    TipiHeader,
    TipiMessage
  },
}
</script>

<style scoped lang="scss">
</style>
