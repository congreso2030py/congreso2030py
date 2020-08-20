<template>
  <div>
    <div v-if="loaded" id="initiative" class="o-container o-section u-margin-bottom-10">
      <div v-if="!initiative.id">
        <div class="o-grid u-padding-top-10 u-padding-bottom-10">
          <div class="o-grid__col u-12 u-10@sm u-offset-1@sm u-text-center u-padding-top-4 u-padding-bottom-4">
            <h1>Expediente no encontrado</h1>
            <p class="u-padding-top-4">Esto puede deberse a que el expediente {{this.$route.params.id}} no tiene relación directa con la Agenda 2030 y sus ODS o que aún no han sido procesados los últimos datos de SILPY. Puedes volver a acceder en unos días para comprobar si ya se ha actualizado.</p>
            <p>Encuentra <router-link :to="{name: 'about'}">más información</router-link> sobre la herramienta o utiliza el <router-link :to="{name:'search'}">buscador</router-link> para encontrar expedientes similares.</p>
          </div>
        </div>
      </div>
      <div v-else>
        <div class="o-grid o-grid--between">
          <div class="o-grid__col u-12 u-8@md">
            <div class="o-grid">
              <div class="o-grid__col u-12 u-6@md">
                <tipi-topic-pill v-if="initiative.topics && initiative.topics.length" class="u-margin-bottom-2" :topicsStyles="styles.topics" :topics="initiative.topics" with-links/>
              </div>
              <div class="o-grid__col u-12 u-6@md u-text-right@md u-margin-bottom-2" v-if="initiative.related && initiative.related.length">
                <a href="#related" class="c-button c-button--compact u-padding-left-0">Ver expedientes relacionados</a>
              </div>
            </div>
            <p class="u-color-secondary u-margin-bottom-1 u-margin-top-0">Actualizado {{ moment(initiative.updated).fromNow() }}</p>
            <h1 class="u-text-th4 u-margin-bottom-4">{{ initiative.title }}</h1>

            <div class="o-grid u-padding-top-4 u-border-top u-border-bottom u-margin-bottom-4">
              <div class="o-grid__col o-grid__col--fill">
                <tipi-text meta="Tipo de acto parlamentario" :value="initiative.initiative_type" />
              </div>
              <div class="o-grid__col u-12 u-3@sm">
                <tipi-text meta="Referencia" :value="initiative.reference" />
              </div>
              <div class="o-grid__col u-12 u-3@sm">
                <tipi-text meta="Registro" :value="moment(initiative.created).format('DD/MM/Y')" />
              </div>
            </div>
            <tipi-topics class="u-hide u-block@md" meta="ODS tratados" :topics="initiative.topics" :tags="initiative.tags" :topicsStyles="styles.topics" />

            <div class="o-grid u-margin-top-4 u-padding-top-4 u-border-top u-hide u-block@md" v-if="initiative.related && initiative.related.length">
              <div class="o-grid__col o-grid__col--fill">
                <h4 id="related" class="u-margin-bottom-4">Expedientes relacionadas</h4>
                <tipi-results :initiatives="initiative.related" :topicsStyles="styles.topics"/>
              </div>
            </div>
          </div>
          <div class="o-grid__col u-12 u-3@md">
            <div class="u-padding-bottom-4 u-border-bottom u-margin-bottom-4">
              <tipi-initiative-meta :initiative="initiative" link-text="Ver en SILpy" :metaColors="metaColors" />
            </div>

            <div class="u-padding-bottom-4 u-border-bottom u-margin-bottom-4">
              <InitiativeChart :initiative="initiative" :topics="allTopics" :styles="styles" v-if="dataLoaded"></InitiativeChart>
              <span class="u-text-tbody2">Relación del expediente con los ODS <sup title="El gráfico muestra los ODS relacionados con este expediente y el grado de relación con cada uno de ellos, cuya intensidad se refleja en la barra circular que los rodea."><i class="fa fa-question-circle"></i></sup></span>
            </div>
            <div class="u-border-bottom u-margin-bottom-4">
              <tipi-text meta="Partido / Otros" :value="initiative.authors" type="parliamentarygroup" :source="allParliamentaryGroups" />
              <tipi-text meta="Legislador/a" :value="initiative.deputies" type="deputy" :source="allDeputies" :hideiGroup="false" />
            </div>
          </div>
        </div>
        <div class="u-hide@md">
          <tipi-topics meta="ODS tratados" :topics="initiative.topics" :tags="initiative.tags" :topicsStyles="styles.topics" />

          <div class="u-margin-top-4 u-padding-top-4 u-border-top" v-if="initiative.related && initiative.related.length">
            <h4 id="related" class="u-margin-bottom-4">Expedientes relacionadas</h4>
            <tipi-results :initiatives="initiative.related" :topicsStyles="styles.topics"/>
          </div>
        </div>
      </div>
    </div>
    <div v-else class="o-container o-section u-margin-bottom-10">
      <tipi-loader title="Cargando datos" subtitle="Puede llevar unos segundos"/>
    </div>
  </div>
</template>

<script>

import { TipiHeader, TipiText, TipiTopics, TipiInitiativeMeta, TipiNeuron, TipiTopicPill, TipiResults, TipiLoader } from 'tipi-uikit'
import api from '@/api';
import config from '@/config';
import { mapState } from 'vuex';
import InitiativeChart from '@/components/initiative-chart.vue';

const moment = require('moment');
moment.locale('es');

export default {
  name: 'initiative',
  components: {
    TipiHeader,
    TipiText,
    TipiTopics,
    TipiInitiativeMeta,
    TipiNeuron,
    TipiTopicPill,
    TipiResults,
    InitiativeChart,
    TipiLoader,
  },
  data: function() {
    return {
      initiative: {},
      moment: moment,
      styles: config.STYLES,
      metaColors: config.COLORIZEDSTATUS,
      loaded: false,
    }
  },
  computed: {
    ...mapState(['allDeputies', 'allTopics', 'allParliamentaryGroups']),
    dataLoaded: function() {
      return (Object.keys(this.initiative).length && this.allTopics.length > 0);
    },
  },
  methods: {
    getInitiative: function() {
      api.getInitiative(this.$route.params.id)
        .then(response => {
          this.initiative = response;
          this.loaded = true;
          window.document.title = window.document.head.querySelector('meta[property="og:title"]').content = window.document.head.querySelector('meta[name="twitter:title"]').content = `${this.initiative.title} - ${config.DEFAULT_PAGE_TITLE}`;
        })
        .catch(error => {
          this.errors = error;
          this.loaded = true;
          // this.$router.push({name: 'InitiativeNotFound', params: { id: this.$route.params.id}});
        });
    },
  },
  created: function() {
    this.getInitiative();
  },
  watch: {
    '$route': 'getInitiative'
  }
}
</script>
