<template>
  <v-row justify="center" align="center">
    <v-col class="d-flex justify-space-between" cols="12" sm="12" md="12">
      <h1 class="h1">Pilotos</h1>
      <v-btn to="/camion/create" color="primary">Crear</v-btn>
    </v-col>
    <vCol>
      <vDataTable
        :headers="[
          { text: 'Id', value: 'id' },
          { text: 'Modelo', value: 'modelo' },
          { text: 'Marca', value: 'marca' },
          { text: 'Placa', value: 'placa' },
          { text: 'Kilometraje', value: 'kilometraje' },
          { text: 'Acciones', value: 'actions', sortable: false }
        ]"
        :items="vehiculos"
        :items-per-page="5"
      >
        <template #[`item.actions`]="{ item }">
          <vTooltip bottom>
            <template #activator="{ on, attrs }">
              <vBtn
                rounded
                small
                v-bind="attrs"
                :to="{ name: 'camion-id', params: { id: item.id } }"
                v-on="on"
              >
                <vIcon small class="mr-2"> mdi-pencil </vIcon>
              </vBtn>
            </template>
            <span>Modificar camion</span>
          </vTooltip>
        </template>
      </vDataTable>
    </vCol>
  </v-row>
</template>
<script>
export default {
  async asyncData({ $axios }) {
    const { vehiculos } = await $axios.$get('/vehiculo')

    return { vehiculos }
  },
  data() {
    return {
      vehiculos: [],
    }
  },
  methods: {},
}
</script>