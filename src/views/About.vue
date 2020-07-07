<template>
  <div>
    <div id="about" class="o-container o-section u-margin-bottom-10">
      <tipi-header title="Acerca"/>
        <div class="o-grid">
          <div class="o-grid__col u-8@sm u-offset-2@sm">

            <p><strong>Congreso2030py</strong> es una innovadora herramienta que rastrea, reúne y ofrece la información sobre la actividad del Congreso Nacional de la República del Paraguay relacionada con los Objetivos de Desarrollo Sostenible. Fue desarrollada para superar los retos que plantea la naturaleza transversal de la Agenda 2030, Congreso 2030Py clasifica la información relacionada con los ODS gracias a un avanzado sistema automático de etiquetado masivo. Esta innovadora tecnología permite a los usuarios navegar por la actividad parlamentaria relacionada con los ODS a través de un buscador online, abierto y gratuito. La información ofrecida es esencial de cara a la monitorización y la rendición de cuentas de la implementación de la Agenda 2030 a nivel nacional.</p>
            <p>La iniciativa ha sido liderada por la Cámara de Senadores del Congreso de Paraguay como parte del Plan de Acción de Parlamento Abierto 2018 – 2020 contraído en el marco de la Asociación de Gobierno Abierto (AGA).</p>
            <p>Ha contado con el apoyo técnico y financiero del Programa de cooperación de la Unión Europea con América Latina, EUROsociAL+, a través de su área de Gobernanza Democrática que coordina la FIIAPP.</p>
            <p>Congreso2030py, al igual que su versión española <a href="http://parlamento2030.es" target="_blank">Parlamento 2030</a>, son proyectos de código abierto desarrollados por el think and do tank español <a href="http://politicalwatch.es" target="_blank">CIECODE/Political Watch</a>. Esta tecnología por su naturaleza abierta, es fácilmente replicable en otros países y regiones.</p>

            <h4>¿Cómo funciona?</h4>
            <p>Congreso2030py reúne toda la información publicada por el Congreso Nacional de la República del Paraguay, a través del SILPY, y crea una base de datos a través de un proceso automático de etiquetado masivo que la clasifica de acuerdo a su relación con cualquier ODS o meta. Combina ciencia informática avanzada - necesaria para escrapear miles de PDFs en los que se publica la información parlamentaria y transformarlos en una base de datos estructurada - con el diseño de unos diccionarios de ODS que automáticamente relacionan iniciativas políticas con objetivos y las metas. Después, a través de un buscador intuitivo, atractivo y accesible, ofrece toda la información relevante en formatos reutilizables. Los usuarios pueden seleccionar sus propios términos en el buscador para adaptar las búsquedas a sus necesidades.</p>

            <h4>¿Qué respuestas ofrece?</h4>
            <p>Congreso2030py ayuda a encontrar las respuestas menos obvias a complicadas preguntas a primera vista: ¿Qué ODS se ven afectados por determinadas iniciativas legislativas? ¿Cuáles objetivos o metas reciben una mayor atención de los diputados y senadores y cuáles son los grandes olvidados? ¿Quiénes son los diputados y senadores más activos en la implementación de la Agenda 2030 y quiénes aportan menos al debate? Además, ofrece un método de gran eficiencia para analizar la actividad política al permitir detectar toda la actividad legislativa relacionada con un determinado ODS o meta propuesta y debatida al mismo tiempo en los diferentes ámbitos del Congreso.</p>

            <h4>¿Por qué el Congreso?</h4>
            <p>Los parlamentos nacionales tienen una posición clave en el proceso de implementación de la Agenda 2030. Son la institución pública más relevante y mejor posicionada para asegurar la coherencia con el desarrollo sostenible en los cientos de miles de leyes, iniciativas legislativas, planes públicos y presupuestos que se aprobarán en cada país en los próximos años.</p>

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
