<template>
  <form id="search-form" class="u-margin-bottom-4 u-border-bottom" role="form" @submit.prevent="getResults($event)">
    <div class="o-grid">
      <div class="o-grid__col u-12 u-padding-bottom-4">
        <div class="c-select-label u-block">
          <label for="topic">ODS</label>
          <multiselect
            selectedLabel="Seleccionado"
            selectLabel=""
            deselectLabel="Pulsa para deseleccionar"
            @select="fillSubtopicsAndTags"
            @remove="clearSubtopicsAndTags"
            v-model="form.topic"
            :options="topics.map(topic => topic.name)"
            :allow-empty="true"
            name="topic" id="topic" placeholder="Todos">
          </multiselect>
        </div>
      </div>
      <div class="o-grid__col u-12 u-6@sm u-padding-bottom-4">
        <div class="c-select-label u-block" :class="{ 'c-select-label--disabled' : !form.topic }">
          <label for="subtopics">Metas</label>
          <multiselect
            selectedLabel="Seleccionada"
            selectLabel=""
            deselectLabel="Pulsa para deseleccionar"
            @select="addSubtopicToTagsFilter"
            @remove="removeSubtopicToTagsFilter"
            v-model="form.subtopics"
            :multiple="true"
            :options="subtopics"
            :allow-empty="true"
            :disabled="!form.topic"
            :placeholder="form.topic ? 'Todos' : 'Selecciona previamente un ODS'"
            name="subtopics" id="subtopics" >
          </multiselect>
        </div>
      </div>
      <div class="o-grid__col u-12 u-6@sm u-padding-bottom-4">
        <div class="c-select-label u-block" :class="{ 'c-select-label--disabled' : !form.topic }">
          <label for="tags">Etiquetas</label>
          <multiselect
          selectedLabel="Seleccionada"
          selectLabel=""
          deselectLabel="Pulsa para deseleccionar"
          v-model="form.tags"
          :multiple="true"
          :options="filteredTags"
          :allow-empty="true"
          :disabled="!form.topic"
          :placeholder="form.topic ? 'Todos' : 'Selecciona previamente un ODS'"
          name="tags" id="tags" >
        </multiselect>
        </div>
      </div>
      <!-- <div class="o&#45;grid__col u&#45;12 u&#45;6@sm u&#45;padding&#45;bottom&#45;4"> -->
      <!--   <div class="c&#45;select&#45;label u&#45;block"> -->
      <!--     <label for="author">Autor</label> -->
      <!--     <multiselect -->
      <!--       selectedLabel="Seleccionado" -->
      <!--       selectLabel="" -->
      <!--       deselectLabel="Pulsa para deseleccionar" -->
      <!--       v&#45;model="form.author" -->
      <!--       :options="groups.map(group => group.name || group)" -->
      <!--       :allow&#45;empty="true" -->
      <!--       name="author" id="author" placeholder="Todos"> -->
      <!--     </multiselect> -->
      <!--   </div> -->
      <!--   <router&#45;link -->
      <!--     class="u&#45;text&#45;tbody2" -->
      <!--     v&#45;if="getParliamentaryGroupByName(form.author)" -->
      <!--     :to="{ path: `/parliamentarygroups/${getParliamentaryGroupByName(form.author).id}` }"> -->
      <!--     ¿Quieres ver el perfil del {{ form.author }}? -->
      <!--   </router&#45;link> -->
      <!-- </div> -->
      <!-- <div class="o&#45;grid__col u&#45;12 u&#45;6@sm u&#45;padding&#45;bottom&#45;4"> -->
      <!--   <div class="c&#45;select&#45;label u&#45;block"> -->
      <!--     <label for="author_deputies">Diputado/a</label> -->
      <!--     <multiselect -->
      <!--       selectedLabel="Seleccionado" -->
      <!--       selectLabel="" -->
      <!--       deselectLabel="Pulsa para deseleccionar" -->
      <!--       v&#45;model="form.deputy" -->
      <!--       :options="deputies" -->
      <!--       :allow&#45;empty="true" -->
      <!--       name="deputy" id="deputy" placeholder="Apellidos, Nombre"> -->
      <!--     </multiselect> -->
      <!--   </div> -->
      <!--   <router&#45;link -->
      <!--     class="u&#45;text&#45;tbody2" -->
      <!--     v&#45;if="getDeputyByName(form.deputy)" -->
      <!--     :to="{ path: `/deputies/${getDeputyByName(form.deputy).id}` }"> -->
      <!--     ¿Quieres ver el perfil de {{ form.deputy }}? -->
      <!--   </router&#45;link> -->
      <!-- </div> -->
    </div> <!-- /.o-grid -->
    <div class="o-grid" v-show="advanced">
      <!-- <div class="o&#45;grid__col u&#45;12 u&#45;4@sm u&#45;padding&#45;bottom&#45;4"> -->
      <!--   <div class="c&#45;datepicker&#45;label u&#45;block"> -->
      <!--     <label for="startdate">Desde</label> -->
      <!--     <datepicker -->
      <!--       v&#45;model="form.startdate" -->
      <!--       @cleared="clearStartDate" -->
      <!--       placeholder="dd/mm/YYYY" format="dd/MM/yyyy" name="startdate"> -->
      <!--     </datepicker> -->
      <!--   </div> -->
      <!-- </div> -->
      <!-- <div class="o&#45;grid__col u&#45;12 u&#45;4@sm u&#45;padding&#45;bottom&#45;4"> -->
      <!--   <div class="c&#45;datepicker&#45;label u&#45;block"> -->
      <!--     <label for="enddate">Hasta</label> -->
      <!--     <datepicker -->
      <!--       v&#45;model="form.enddate" -->
      <!--       @cleared="clearEndDate" -->
      <!--       placeholder="dd/mm/YYYY" format="dd/MM/yyyy" name="enddate"> -->
      <!--     </datepicker> -->
      <!--   </div> -->
      <!-- </div> -->
      <!-- <div class="o&#45;grid__col u&#45;12 u&#45;4@sm u&#45;padding&#45;bottom&#45;4"> -->
      <!--   <div class="c&#45;select&#45;label u&#45;block"> -->
      <!--     <label for="status">Estado</label> -->
      <!--     <multiselect -->
      <!--       selectedLabel="Seleccionado" -->
      <!--       selectLabel="" -->
      <!--       deselectLabel="Pulsa para deseleccionar" -->
      <!--       v&#45;model="form.status" -->
      <!--       :options="status" -->
      <!--       :allow&#45;empty="true" -->
      <!--       name="status" id="status" placeholder="Cualquiera"> -->
      <!--     </multiselect> -->
      <!--   </div> -->
      <!-- </div> -->
      <!-- <div class="o&#45;grid__col u&#45;12 u&#45;6@sm u&#45;padding&#45;bottom&#45;4"> -->
      <!--   <div class="c&#45;select&#45;label u&#45;block"> -->
      <!--     <label for="place">Lugar</label> -->
      <!--     <multiselect -->
      <!--       selectedLabel="Seleccionado" -->
      <!--       selectLabel="" -->
      <!--       deselectLabel="Pulsa para deseleccionar" -->
      <!--       v&#45;model="form.place" -->
      <!--       :options="places" -->
      <!--       :allow&#45;empty="true" -->
      <!--       name="place" id="place" placeholder="Cualquiera"> -->
      <!--     </multiselect> -->
      <!--   </div> -->
      <!-- </div> -->
      <!-- <div class="o&#45;grid__col u&#45;12 u&#45;6@sm u&#45;padding&#45;bottom&#45;4"> -->
      <!--   <div class="c&#45;select&#45;label u&#45;block"> -->
      <!--     <label for="type">Tipo</label> -->
      <!--     <multiselect -->
      <!--       selectedLabel="Seleccionado" -->
      <!--       selectLabel="" -->
      <!--       deselectLabel="Pulsa para deseleccionar" -->
      <!--       v&#45;model="form.type" -->
      <!--       :options="types" -->
      <!--       :allow&#45;empty="true" -->
      <!--       name="type" id="type" placeholder="Cualquiera"> -->
      <!--     </multiselect> -->
      <!--   </div> -->
      <!-- </div> -->
      <!-- <div class="o&#45;grid__col u&#45;12 u&#45;6@sm u&#45;padding&#45;bottom&#45;4"> -->
      <!--   <div class="c&#45;input&#45;label u&#45;block"> -->
      <!--     <label for="reference">Referencia</label> -->
      <!--     <input v&#45;model="form.reference" type="text" id="reference" name="reference" placeholder="Ej.: 121/000001"> -->
      <!--   </div> -->
      <!-- </div> -->
      <!-- <div class="o&#45;grid__col u&#45;12 u&#45;6@sm u&#45;padding&#45;bottom&#45;4"> -->
      <!--   <div class="c&#45;input&#45;label u&#45;block"> -->
      <!--     <label for="title">Título</label> -->
      <!--     <input v&#45;model="form.title" type="text" id="title" name="title" placeholder="Nota: Se admiten expresiones regulares"> -->
      <!--   </div> -->
      <!-- </div> -->
    </div> <!-- /.o-grid -->
    <div class="o-grid">
      <div class="o-grid__col u-12 u-6@sm u-padding-bottom-4">
        <!-- <a href="#" class="c&#45;button u&#45;padding&#45;left&#45;0" @click.prevent="toggleAdvanced"> -->
        <!--   <tipi&#45;icon icon="advanced" /> -->
        <!--   <span v&#45;if="!advanced">Mostrar búsqueda avanzada</span> -->
        <!--   <span v&#45;else>Ocultar búsqueda avanzada</span> -->
        <!-- </a> -->
      </div>
      <div class="o-grid__col u-12 u-6@sm u-padding-bottom-4 u-text-right@sm">
        <button class="c-button u-padding-left-0 u-margin-right-2" @click.prevent="cleanForm">Limpiar búsqueda</button>
        <button class="c-button c-button--primary" type="submit">Buscar</button>
      </div>
    </div>
  </form>
</template>

<script>
import Datepicker from 'vuejs-datepicker';
import Multiselect from 'vue-multiselect'
import { TipiIcon } from 'tipi-uikit';
import api from '@/api'
import { mapGetters, mapState } from 'vuex';
// eslint-disable-next-line no-unused-vars
import assign from "core-js/features/object/assign";

const moment = require('moment');

export default {
  name: 'searchForm',
  components: {
    Datepicker,
    Multiselect,
    TipiIcon,
  },
  props: {
    formData: Object,
  },
  data: function() {
    return {
      subtopics: [],
      tags: [],
      form: {},
      errors: null,
      moment: moment,
      selectedSubtopics: [],
      filteredTags: [],
      advanced: this.formData && (this.formData.startdate || this.formData.enddate || this.formData.status || this.formData.place || this.formData.type || this.formData.reference || this.formData.title),
    }
  },
  computed: {
    ...mapGetters({
      deputies: 'allDeputiesName',
      places: 'allPlacesName',
      groups: 'allParliamentaryGroupsWithGoverment',
      getDeputyByName: 'getDeputyByName',
      getParliamentaryGroupByName: 'getParliamentaryGroupByName',
    }),
    ...mapState({
      topics: 'allTopics',
      types: 'allTypes',
      status: 'allStatus',
    })
  },
  methods: {
    cleanForm: function() {
      this.form.topic =
      this.form.subtopics =
      this.form.tags =
      this.form.author =
      this.form.deputy =
      this.form.status =
      this.form.place =
      this.form.type =
      this.form.reference =
      this.form.enddate =
      this.form.startdate =
      this.form.title = '';
    },
    fillSubtopicsAndTags: function(selectedTopic, clearValues) {
      if (clearValues) {
        this.form.subtopics = [];
        this.form.tags = [];
      }
      const currentTopic = this.topics.find(topic => topic.name === selectedTopic);
      this.getSubtopicsAndTags(currentTopic.id);
    },
    clearSubtopicsAndTags: function() {
      this.subtopics = [];
      this.selectedSubtopics = [];
      this.tags = [];
      this.filteredTags = [];
      this.form.subtopics = [];
      this.form.tags = [];
    },
    clearStartDate: function() {
      this.form.startdate = '';
    },
    clearEndDate: function() {
      this.form.enddate = '';
    },
    getSubtopicsAndTags: function(topicID) {
      api.getTags(topicID)
        .then(tags => {
          this.subtopics = [...new Set(tags.map(tag => tag.subtopic))];
          this.tags = tags;
          this.filteredTags = this.tags.map(tag => tag.tag);
        })
        .catch(error => this.errors = error);
    },
    filterTags: function() {
      let filtered = (this.selectedSubtopics.length) ?
        (tag => this.selectedSubtopics.indexOf(tag.subtopic) !== -1)
        : (() => true);
      this.filteredTags = this.tags.filter(filtered).map(tag => tag.tag);
    },
    addSubtopicToTagsFilter: function(selectedSubtopic) {
      this.form.tags = [];
      this.selectedSubtopics.push(selectedSubtopic);
      this.filterTags();
    },
    removeSubtopicToTagsFilter: function(removedSubtopic) {
      this.form.tags = [];
      this.selectedSubtopics.splice(this.selectedSubtopics.indexOf(removedSubtopic), 1);
      this.filterTags();
    },
    getResults: function(event) {
      this.form.enddate = this.form.enddate ? moment(this.form.enddate).format('YYYY-MM-DD') : undefined;
      this.form.startdate = this.form.startdate ? moment(this.form.startdate).format('YYYY-MM-DD') : undefined;
      this.$emit('getResults', event, this.form);
    },
    prepareForm: function() {
      if (this.form.topic) {
        this.fillSubtopicsAndTags(this.form.topic, false);
      }
    },
    toggleAdvanced: function() {
      this.advanced = !this.advanced;
    }
  },
  created: function() {
    this.form = Object.assign({}, this.formData);
    if (this.topics.length) {
      this.prepareForm();
    }
  },
}
</script>
