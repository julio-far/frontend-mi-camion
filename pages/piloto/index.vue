<template>
  <v-row justify="center" align="center">
    <v-col class="d-flex justify-space-between" cols="12" sm="12" md="12">
      <h1 class="h1">Pilotos</h1>
      <v-btn color="primary">Crear</v-btn>
    </v-col>
    <vCol>
      <vDataTable
        :headers="[
          { text: 'Id', value: 'id' },
          { text: 'Nombre', value: 'nombre' },
          { text: 'DPI', value: 'dpi' },
          { text: 'Licencia', value: 'licencia' },
          { text: 'Teléfono', value: 'telefono' }
        ]"
        :items="pilotos"
        rows-per-page-items="5"
      ></vDataTable>
    </vCol>
  </v-row>
</template>
<script>
export default {
  async asyncData({ $axios }) {
    const { pilotos } = await $axios.$get('/piloto')

    return { pilotos }
  },
  data() {
    return {
      pilotos: [],
    }
  },
  methods: {},
}
</script>