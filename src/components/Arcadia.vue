<template>
  <section>
    <q-layout container style="height: 100vh">
      <q-drawer v-model="drawer" show-if-above elevated :mini="true">
        <q-scroll-area class="fit">
          <q-list padding>
            <q-item clickable>
              <q-item-section avatar>
                <q-icon name="menu" />
              </q-item-section>
            </q-item>
            <q-item clickable @click="menuSearch = !menuSearch">
              <q-item-section avatar>
                <q-icon name="search" />
              </q-item-section>
            </q-item>
            <q-item clickable @click="menuLayer = !menuLayer">
              <q-item-section avatar>
                <q-icon name="layers" />
              </q-item-section>
            </q-item>
            <q-item clickable>
              <q-item-section avatar>
                <q-icon name="print" />
              </q-item-section>
            </q-item>
          </q-list>
        </q-scroll-area>
      </q-drawer>
      <q-page-container>
        <q-page>
          <q-layout container style="height: 100vh">
            <q-drawer
              v-model="menuSearch"
              overlay
              side="left"
              elevated
              :width="400"
            >
              <q-scroll-area class="fit">
                <section class="q-pa-md">
                  <q-input
                    filled
                    v-model="search"
                    placeholder="Buscar lugares, capas, objetos"
                    @input="searchLocation"
                    :loading="searchLoading"
                  >
                    <template v-slot:prepend>
                      <q-icon name="search" />
                    </template>
                  </q-input>
                  <div v-if="!search">
                    <div class="q-mt-md q-mb-md">
                      <span class="text-subtitle1">Últimas búsquedas</span>
                    </div>
                    <q-list :padding="false">
                      <q-item clickable v-ripple>
                        <q-item-section avatar top>
                          <q-avatar color="blue" icon="place" />
                        </q-item-section>
                        <q-item-section>
                          <q-item-label lines="1">Loreto</q-item-label>
                          <q-item-label caption>12/11/2016 12:12</q-item-label>
                        </q-item-section>
                      </q-item>
                    </q-list>
                    <q-separator class="q-mt-md"></q-separator>
                    <div class="q-mt-md q-mb-md">
                      <span class="text-subtitle1">Mis lugares</span>
                    </div>
                    <q-list :padding="false">
                      <q-item clickable v-ripple>
                        <q-item-section avatar top>
                          <q-avatar color="red" icon="place" />
                        </q-item-section>
                        <q-item-section>
                          <q-item-label lines="1">Loreto</q-item-label>
                          <q-item-label caption>12/11/2016 12:12</q-item-label>
                        </q-item-section>
                        <q-item-section side>
                          <q-icon color="white" name="edit" />
                        </q-item-section>
                      </q-item>
                    </q-list>
                  </div>
                  <div v-if="search">
                    <div class="q-mt-md q-mb-md">
                      <span class="text-subtitle1">Lugares</span>
                    </div>
                    <q-list
                      :padding="false"
                      v-for="suggestion in suggestions"
                      v-bind:key="suggestion.magicKey"
                    >
                      <q-item
                        clickable
                        v-ripple
                        @click="zoomToLocation(suggestion.magicKey)"
                      >
                        <q-item-section avatar>
                          <q-avatar color="blue" icon="place" />
                        </q-item-section>
                        <q-item-section>{{ suggestion.text }}</q-item-section>
                      </q-item>
                    </q-list>
                    <div class="q-mt-md q-mb-md">
                      <span class="text-subtitle1">Capas</span>
                    </div>
                  </div>
                </section>
              </q-scroll-area>
            </q-drawer>
            <q-drawer
              v-model="menuLayer"
              overlay
              side="left"
              elevated
              :width="400"
            >
              <q-scroll-area class="fit">
                <section class="q-pa-md">
                  <q-input
                    filled
                    v-model="filter"
                    placeholder="Buscar capas"
                    @input="filter"
                    class="q-mb-md"
                  >
                    <template v-slot:prepend>
                      <q-icon name="search" />
                    </template>
                  </q-input>
                  <q-tree
                    :filter="filter"
                    :nodes="layers"
                    node-key="label"
                    tick-strategy="leaf"
                  />
                </section>
              </q-scroll-area>
            </q-drawer>
            <q-page-container>
              <q-page>
                <section class="container">
                  <q-card class="card">
                    <q-img src="https://cdn.quasar.dev/img/chicken-salad.jpg" />
                    <q-card-section>
                      <q-btn
                        fab
                        color="primary"
                        icon="place"
                        class="absolute"
                        style="top: 0; right: 12px; transform: translateY(-50%);"
                      />

                      <div class="row no-wrap items-center">
                        <div class="col text-h6 ellipsis">
                          Cafe Basilico
                        </div>
                        <div
                          class="col-auto text-grey text-caption q-pt-md row no-wrap items-center"
                        >
                          <q-icon name="place" />
                          250 ft
                        </div>
                      </div>

                      <q-rating v-model="stars" :max="5" size="32px" />
                    </q-card-section>

                    <q-card-section class="q-pt-none">
                      <div class="text-subtitle1">
                        $・Italian, Cafe
                      </div>
                      <div class="text-caption text-grey">
                        Small plates, salads & sandwiches in an intimate
                        setting.
                      </div>
                    </q-card-section>

                    <q-separator />

                    <q-card-actions>
                      <q-btn flat round icon="event" />
                      <q-btn flat color="primary">
                        Reserve
                      </q-btn>
                    </q-card-actions>
                  </q-card>
                  <div id="map"></div>
                </section>
              </q-page>
            </q-page-container>
          </q-layout>
        </q-page>
      </q-page-container>
    </q-layout>
  </section>
</template>
<script>
import L from 'leaflet';
import axios from 'axios';
import 'leaflet/dist/leaflet.css';
export default {
  data() {
    return {
      stars: 4,

      map: null,
      searchLoading: false,
      search: '',
      drawer: true,
      menuSearch: false,
      menuLayer: false,
      expanded: false,
      filter: null,
      latitude: 0,
      longitude: 0,
      title: '',
      description: '',
      suggestions: [],
      layers: [
        {
          label: 'Transportes y telecomunicaciones',
          children: [
            {
              label: 'Ferrocarriles'
            }
          ]
        },
        {
          label: 'Medio ambiente'
        }
      ]
    };
  },
  mounted() {
    this.map = L.map('map').setView([51.505, -0.09], 13);
    const baseLayer = L.tileLayer(
      'https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}'
    );
    this.map.addLayer(baseLayer);
  },
  methods: {
    searchLocation() {
      this.searchLoading = true;
      let url =
        'https://geocode.arcgis.com/arcgis/rest/services/World/GeocodeServer/suggest?f=json&langCode=es&';
      url += `text=${this.search}`;
      axios.get(url).then(response => {
        this.searchLoading = false;
        this.suggestions = response.data.suggestions;
      });
    },
    zoomToLocation(magicKey) {
      let url =
        'http://geocode.arcgis.com/arcgis/rest/services/World/GeocodeServer/findAddressCandidates?f=json&langCode=spa&outFields=*&';
      url += `magicKey=${magicKey}`;
      axios.get(url).then(response => {
        const result = response.data.candidates[0];
        this.map.setView([result.location.y, result.location.x], 13);
        this.menuSearch = false;
        this.search = '';
      });
    }
  }
};
</script>

<style lang="sass">
.container
  position: relative
  height: 100vh
#map
  z-index: 0
  position: absolute
  height: 100%
  width: 100%

.leaflet-bar a, .leaflet-bar a:hover
  background-color: #1d1d1d !important
  border-bottom: 1px solid #1d1d1d !important
  color: white !important

.card
  width: 300px
  max-width: 300px
  position: absolute
  z-index: 1
  top: 20px
  right: 20px
</style>
