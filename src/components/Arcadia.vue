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
            </q-drawer>
            <q-drawer v-model="menuLayer" side="left" elevated :width="400">
              <div class="q-pa-sm">
                <q-card>
                  <q-toolbar class="bg-blue text-white">
                    <q-input
                      class="block"
                      dark
                      borderless
                      v-model="filter"
                      placeholder="Buscar"
                    >
                      <template v-slot:append>
                        <q-icon v-if="!filter" name="search" />
                      </template>
                    </q-input>
                  </q-toolbar>
                  <q-card-section>
                    <q-tree
                      :filter="filter"
                      :nodes="layers"
                      node-key="label"
                      tick-strategy="leaf"
                    />
                  </q-card-section>
                </q-card>
              </div>
            </q-drawer>
            <q-page-container>
              <q-page>
                <div id="map"></div>
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
      'https://mt1.google.com/vt/lyrs=r&x={x}&y={y}&z={z}'
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
#map
  height: 100vh

.leaflet-bar a, .leaflet-bar a:hover
  background-color: #1d1d1d !important
  border-bottom: 1px solid #1d1d1d !important
  color: white !important
</style>
