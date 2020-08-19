<template>
  <div>
    <div id="group" class="o-container o-section u-margin-bottom-10">
      <tipi-header v-if="parliamentarygroup" :title="parliamentarygroup.name"/>
      <div v-if="latestInitiatives && latestInitiatives.length" class="o-container o-section u-margin-bottom-4">
        <h4 class="u-margin-bottom-4">Últimos expedientes</h4>
        <tipi-results layout="tiny" :initiatives="latestInitiatives" :topicsStyles="topicsStyles"/>
      </div>
      <div class="o-container o-section" v-else>
        <tipi-message type="info" icon>
          Sin actividad parlamentaria relacionada con la Agenda 2030 en esta legislatura
        </tipi-message>
      </div>

      <div class="o-container o-section">
        <h4 class="u-margin-bottom-4">Legisladores/as en activo</h4>
        <div class="o-grid" v-if="this.activeDeputies.length > 0">
          <div class="o-grid__col u-12 u-4@sm">
            <tipi-text meta="" :value="this.dividedActiveDeputies[0]" type="deputy" :source="allDeputies" hideGroup/>
          </div>
          <div class="o-grid__col u-12 u-4@sm">
            <tipi-text meta="" :value="this.dividedActiveDeputies[1]" type="deputy" :source="allDeputies" hideGroup/>
          </div>
          <div class="o-grid__col u-12 u-4@sm">
            <tipi-text meta="" :value="this.dividedActiveDeputies[2]" type="deputy" :source="allDeputies" hideGroup/>
          </div>
        </div>
        <div class="o-grid" v-else>
          <tipi-message type="info" icon>
            No se han encontrado legisladores/as en activo para este partido
          </tipi-message>
        </div>
      </div>

      <div class="o-container o-section">
        <h4 class="u-margin-bottom-4">Legisladores/as antiguos/as</h4>
        <div class="o-grid" v-if="this.inactiveDeputies.length > 0">
          <div class="o-grid__col u-12 u-4@sm">
            <tipi-text meta="" :value="this.dividedInactiveDeputies[0]" type="deputy" :source="allDeputies" hideGroup/>
          </div>
          <div class="o-grid__col u-12 u-4@sm">
            <tipi-text meta="" :value="this.dividedInactiveDeputies[1]" type="deputy" :source="allDeputies" hideGroup/>
          </div>
          <div class="o-grid__col u-12 u-4@sm">
            <tipi-text meta="" :value="this.dividedInactiveDeputies[2]" type="deputy" :source="allDeputies" hideGroup/>
          </div>
        </div>
        <div class="o-grid" v-else>
          <tipi-message type="info" icon>
            No se han encontrado legisladores/as antiguos/as para este partido
          </tipi-message>
        </div>
      </div>

    </div>
  </div>
</template>

<script>

import { TipiHeader, TipiMessage, TipiResults, TipiText } from 'tipi-uikit'
import api from '@/api';
import config from '@/config'
import { mapGetters, mapState } from  'vuex';

export default {
  name: 'parliamentarygroup',
  components: {
    TipiHeader,
    TipiMessage,
    TipiResults,
    TipiText,
  },
  data: function() {
    return {
      parliamentarygroup: null,
      latestInitiatives: null,
      topicsStyles: config.STYLES.topics,
    }
  },
  computed: {
    ...mapState(['allDeputies']),
    ...mapGetters(['getDeputiesByParliamentaryGroup']),
    activeDeputies: function () {
      if (this.parliamentarygroup) {
        return this.filterDeputiesBy(this.parliamentarygroup, true);
      }
      return [];
    },
    inactiveDeputies: function () {
      if (this.parliamentarygroup) {
        return this.filterDeputiesBy(this.parliamentarygroup, false);
      }
      return [];
    },
    dividedActiveDeputies: function() {
      return this.divide(this.activeDeputies);
    },
    dividedInactiveDeputies: function() {
      return this.divide(this.inactiveDeputies);
    }
  },
  methods: {
    getParliamentaryGroup: function() {
      api.getGroup(this.$route.params.id)
        .then(response => {
          this.parliamentarygroup = response;
          this.getLatestInitiatives();
        })
        .catch(error => {
          this.errors = error
          this.$router.push({name: 'Page404', params: { '0': '404'}});
        });
    },
    getLatestInitiatives: function() {
      api.getInitiatives({'author': this.parliamentarygroup.name, 'per_page': 12 })
         .then(response => {
           if (response.initiatives) this.latestInitiatives = response.initiatives;
          })
         .catch(error => this.errors = error);
    },
    filterDeputiesBy: function(parliamentarygroup, status) {
      return this.getDeputiesByParliamentaryGroup(parliamentarygroup.shortname)
        .filter(deputy => deputy.active == status)
        .map(deputy => deputy.name + '[' + deputy.id + ']');
    },
    divide: function(deputies) {
      let results = [];
      let divided = deputies.slice();
      for (let i = 3; i > 0; i--) {
        results.push(divided.splice(0, Math.ceil(divided.length/i)));
      }
      return results;
    }
  },
  created: function() {
    this.getParliamentaryGroup()
  }
}
</script>
