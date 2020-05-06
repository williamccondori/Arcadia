<template>
  <div>
    <img
      alt=""
      class="style-icon"
      slot="icon"
      src="data:image/svg+xml;utf8,%0A%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20xmlns%3Axlink%3D%22http%3A%2F%2Fwww.w3.org%2F1999%2Fxlink%22%20viewBox%3D%220%200%2072%2094%22%3E%0A%20%20%3Cdefs%3E%0A%20%20%20%20%3ClinearGradient%20id%3D%22d%22%20x1%3D%2250%25%22%20x2%3D%220%25%22%20y1%3D%2254.9%25%22%20y2%3D%22100%25%22%3E%0A%20%20%20%20%20%20%3Cstop%20offset%3D%220%25%22%20stop-color%3D%22%23E1E2E6%22%2F%3E%0A%20%20%20%20%20%20%3Cstop%20offset%3D%22100%25%22%20stop-color%3D%22%23C9CCD0%22%2F%3E%0A%20%20%20%20%3C%2FlinearGradient%3E%0A%20%20%20%20%3ClinearGradient%20id%3D%22e%22%20x1%3D%2250%25%22%20x2%3D%22100%25%22%20y1%3D%2250%25%22%20y2%3D%220%25%22%3E%0A%20%20%20%20%20%20%3Cstop%20offset%3D%220%25%22%20stop-color%3D%22%23ADB0B8%22%2F%3E%0A%20%20%20%20%20%20%3Cstop%20offset%3D%22100%25%22%20stop-color%3D%22%23B7B9C2%22%2F%3E%0A%20%20%20%20%3C%2FlinearGradient%3E%0A%20%20%20%20%3Ccircle%20id%3D%22a%22%20cx%3D%2232.1%22%20cy%3D%2232.1%22%20r%3D%2232.1%22%2F%3E%0A%20%20%20%20%3Cpath%20id%3D%22c%22%20d%3D%22M2%200a2%202%200%20104%200h2a2%202%200%20104%200h2a2%202%200%20104%200h2a2%202%200%20104%200h2a2%202%200%20104%200h2v32H6.5L0%2025.5V0h2z%22%2F%3E%0A%20%20%3C%2Fdefs%3E%0A%20%20%3Cg%20fill%3D%22none%22%20fill-rule%3D%22evenodd%22%3E%0A%20%20%20%20%3Cg%20transform%3D%22translate(11.7%202.2)%22%3E%0A%20%20%20%20%20%20%3Cpath%20stroke%3D%22%2380868B%22%20stroke-linecap%3D%22round%22%20stroke-width%3D%223%22%20d%3D%22M4%2075.3L36.9.2%22%2F%3E%0A%20%20%20%20%20%20%3Cpath%20fill%3D%22%235F6368%22%20d%3D%22M59.7%2037.7A39.2%2039.2%200%20010%2071l1.3-2.8A36.1%2036.1%200%201030.4%202.8L31.6.2a39.2%2039.2%200%200128.1%2037.6z%22%2F%3E%0A%20%20%20%20%20%20%3Cpath%20stroke%3D%22%235F6368%22%20stroke-linecap%3D%22round%22%20stroke-width%3D%223%22%20d%3D%22M20.6%2075.4v11%22%2F%3E%0A%20%20%20%20%20%20%3Ccircle%20cx%3D%2220.4%22%20cy%3D%2275.3%22%20r%3D%222.9%22%20fill%3D%22%233C4043%22%2F%3E%0A%20%20%20%20%20%20%3Cpath%20fill%3D%22%233C4043%22%20d%3D%22M17.7%2092C18%2085.2%2019%2081.8%2020.6%2082c1.6-.2%202.5%203.2%202.8%2010.2h-5.7z%22%2F%3E%0A%20%20%20%20%20%20%3Cpath%20fill%3D%22%235F6368%22%20d%3D%22M4.4%2092.8c5.8-3.4%2011.4-5%2016.6-5a29%2029%200%200115.7%205%22%2F%3E%0A%20%20%20%20%3C%2Fg%3E%0A%20%20%20%20%3Cg%20transform%3D%22translate(0%207.7)%22%3E%0A%20%20%20%20%20%20%3Cmask%20id%3D%22b%22%20fill%3D%22%23fff%22%3E%0A%20%20%20%20%20%20%20%20%3Cuse%20xlink%3Ahref%3D%22%23a%22%2F%3E%0A%20%20%20%20%20%20%3C%2Fmask%3E%0A%20%20%20%20%20%20%3Cuse%20fill%3D%22%23B2CEFA%22%20xlink%3Ahref%3D%22%23a%22%2F%3E%0A%20%20%20%20%20%20%3Ccircle%20cx%3D%2240.7%22%20cy%3D%2224.8%22%20r%3D%2232.1%22%20fill%3D%22%23D2E3FC%22%20mask%3D%22url(%23b)%22%2F%3E%0A%20%20%20%20%20%20%3Cpath%20fill%3D%22%2377CC8E%22%20fill-rule%3D%22nonzero%22%20d%3D%22M39.6%2058.6c1.9-2%202-5.1%200-7.2a6.6%206.6%200%2001-1-6.6l1-2.2c.8-1.8.2-3.8-1.3-4.9L24%2028.1a6.7%206.7%200%2001-2-8.8l2.3-4.4c.7-1.3.5-2.8-.5-3.8%200%200-3-3.5-2.6-5.6%201.5-6.4%208.1-4.4%209.4-7l1.5-3%2016.6%206.1-2.5%204.1a2%202%200%20001%203l3.3%201.2a.7.7%200%20010%201.4L47%2012.7c-1.1.4-2%201.2-2.5%202.3a3%203%200%20001.1%203.9l4.6%202.9c1.5%201%202.5%202.6%202.6%204.4v.2a4.8%204.8%200%2001-4.9%204.9l-7.3-.1c-1.2%200-1.8%201.6-.7%202.3l4.3%203c1.4%201%202%202.8%201.4%204.5l-.4%201.3c-.7%202%20.1%204%202%205l6%203.4a4.8%204.8%200%20011%207.7L48%2064.3l-17.7%204.1%209.3-9.8z%22%20mask%3D%22url(%23b)%22%2F%3E%0A%20%20%20%20%20%20%3Cpath%20fill%3D%22%2366B17B%22%20fill-rule%3D%22nonzero%22%20d%3D%22M13.1%2063.2l2.2-7.3c1.1-4-1-8-5-9.2l-4-1.3A2%202%200%20015%2042.6l3.3-6.3a7%207%200%2000-.4-7L7.3%2028c-1.3-2-3.7-3.1-6-2.9l-10.7%201.2%205.5%2025.2%2017%2011.6z%22%20mask%3D%22url(%23b)%22%2F%3E%0A%20%20%20%20%3C%2Fg%3E%0A%20%20%20%20%3Cg%3E%0A%20%20%20%20%20%20%3Cg%20transform%3D%22translate(29.5%2048)%22%3E%0A%20%20%20%20%20%20%20%20%3Cmask%20id%3D%22f%22%20fill%3D%22%23fff%22%3E%0A%20%20%20%20%20%20%20%20%20%20%3Cuse%20xlink%3Ahref%3D%22%23c%22%2F%3E%0A%20%20%20%20%20%20%20%20%3C%2Fmask%3E%0A%20%20%20%20%20%20%20%20%3Cuse%20fill%3D%22url(%23d)%22%20xlink%3Ahref%3D%22%23c%22%2F%3E%0A%20%20%20%20%20%20%20%20%3Cpath%20fill%3D%22url(%23e)%22%20d%3D%22M0%2025.5h6.5V32H0z%22%20mask%3D%22url(%23f)%22%2F%3E%0A%20%20%20%20%20%20%3C%2Fg%3E%0A%20%20%20%20%20%20%3Cg%20stroke%3D%22%2334A853%22%20stroke-linecap%3D%22round%22%3E%0A%20%20%20%20%20%20%20%20%3Cpath%20d%3D%22M34.1%2058.1l1.4%201.4M35.5%2059.5l2.7-2.7%22%2F%3E%0A%20%20%20%20%20%20%3C%2Fg%3E%0A%20%20%20%20%20%20%3Cg%20stroke%3D%22%2334A853%22%20stroke-linecap%3D%22round%22%3E%0A%20%20%20%20%20%20%20%20%3Cpath%20d%3D%22M34.1%2065.1l1.4%201.4M35.5%2066.5l2.7-2.7%22%2F%3E%0A%20%20%20%20%20%20%3C%2Fg%3E%0A%20%20%20%20%20%20%3Cpath%20stroke%3D%22%23686C71%22%20stroke-linecap%3D%22round%22%20d%3D%22M42.5%2058.5h13M42.5%2065.5h13M42.5%2072.5h13%22%2F%3E%0A%20%20%20%20%3C%2Fg%3E%0A%20%20%3C%2Fg%3E%0A%3C%2Fsvg%3E"
    />
    <div class="row q-mb-sm">
      <div class="col">
        <q-card>
          <q-toolbar class="bg-dark text-white">
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
    </div>
    <div class="row q-mb-sm">
      <div class="col">
        <q-input outlined v-model="title" label="Título" stack-label />
      </div>
    </div>
    <div class="row q-mb-sm">
      <div class="col">
        <q-editor v-model="description" min-height="5rem" />
      </div>
    </div>
    <div class="row">
      <div class="col">
        <q-expansion-item label="Ubicación">
          <div class="row q-col-gutter-sm">
            <div class="col">
              <q-input
                outlined
                v-model="latitude"
                label="Latitud"
                stack-label
                type="number"
              />
            </div>
            <div class="col">
              <q-input
                outlined
                v-model="longitude"
                label="Longitud"
                stack-label
                type="number"
              />
            </div>
          </div>
        </q-expansion-item>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      expanded: false,
      filter: null,
      latitude: 0,
      longitude: 0,
      title: '',
      description: '',
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
  }
};
</script>

<style lang="sass" scoped>
.block
    width: 100%
</style>
