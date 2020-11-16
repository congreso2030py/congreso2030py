<template>
  <div>
    <div id="footer" class="o-container o-container--fluid o-section u-bg-secondary-light">

      <div class="o-container">
        <div class="o-grid">
          <div class="o-grid__col u-3@sm u-margin-top-4">
            <p class="u-text-overline">Impulsado por</p>
            <img src="/img/congresopy.png" class="big" alt="Logo del Congreso de la Nación Paraguay">
          </div>
          <div class="o-grid__col u-4@sm u-offset-1@sm u-margin-top-4">
            <p class="u-text-overline">Con el apoyo de</p>
            <img src="/img/ue-eurosocial.png" class="big" alt="Logo de la Unión Europea y Eurosocial">
          </div>
          <div class="o-grid__col u-3@sm u-offset-1@sm u-margin-top-4">
            <p class="u-text-overline">Desarrollado por</p>
            <div class="o-grid">
              <div class="o-grid__col u-8@xs">
                <a href="http://politicalwatch.es"><img src="/img/politicalwatch.png" class="big" alt="Logo de Political Watch"></a>
              </div>
            </div>
          </div>
        </div>

        <div class="o-container u-margin-top-4">
          <div class="o-grid">
            <div class="o-grid__col u-12@sm text-center u-text-tbody2" style="text-align: center;">
              Todo el código fuente está disponible en <a href="https://github.com/politicalwatch" target="_blank">GitHub</a> con licencia <a href="https://www.gnu.org/licenses/gpl-3.0.html" target="_blank">GNU/GPLv3</a>
              <br>
              Contacta con nosotras en <a href="mailto:congreso2030@senado.gov.py" target="_blank">congreso2030@senado.gov.py</a> · <a href="congreso2030@diputados.gov.py" target="_blank">congreso2030@diputados.gov.py</a>
            </div>
          </div>
        </div>

      </div>

    </div>

    <div class="c-decorator" style="background-image: url('/img/multicolor.jpg')"></div>

    <cookie-law theme="base" buttonText="Entendido" buttonClass="btn btn-custom" message="Este sitio usa cookies para asegurarte la mejor experiencia web."></cookie-law>

  </div>
</template>

<script>
  import CookieLaw from 'vue-cookie-law';

export default {
  name: "footer-block",
  components: {CookieLaw}
}
</script>

<style scoped lang="scss">
</style>
