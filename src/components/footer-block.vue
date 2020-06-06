<template>
  <div>
    <div id="footer" class="o-container o-container--fluid o-section u-bg-secondary-light">
      <div class="o-grid">
        <div class="o-grid__col u-12@sm">
          <div class="o-container">
            <div class="o-grid">
              <div class="o-grid__col u-3@sm text-center">
                <a href="/"><img src="/img/logo.png" class="big" alt="Logo de Congreso 2030 Paraguay"></a>
              </div>
              <div class="o-grid__col u-8@sm u-offset-1@sm u-text-tbody2">
              </div>
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
