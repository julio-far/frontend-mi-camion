<template>
  <v-row justify="center" align="center">
    <v-col class="d-flex justify-space-between" cols="12" sm="12" md="12">
      <h1 class="h1">Pilotos</h1>
      <v-btn to="/piloto/create" color="primary">Crear</v-btn>
    </v-col>
    <vCol>
      <vDataTable
        :headers="[
          { text: 'Id', value: 'id' },
          { text: 'Nombre', value: 'nombre' },
          { text: 'DPI', value: 'dpi' },
          { text: 'Licencia', value: 'licencia' },
          { text: 'Teléfono', value: 'telefono' },
          { text: 'Acciones', value: 'actions', sortable: false }
        ]"
        :items="pilotos"
        :items-per-page="5"
      >
        <template #[`item.actions`]="{ item }">
          <vTooltip bottom>
            <template #activator="{ on, attrs }">
              <vBtn
                rounded
                small
                v-bind="attrs"
                :to="{ name: 'piloto-id', params: { id: item.id } }"
                v-on="on"
              >
                <vIcon small class="mr-2"> mdi-pencil </vIcon>
              </vBtn>
            </template>
            <span>Modificar cita</span>
          </vTooltip>
        </template>
      </vDataTable>
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