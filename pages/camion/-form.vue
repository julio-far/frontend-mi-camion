<template>
  <v-row justify="center" align="center">
    <v-col class="d-flex justify-space-between" cols="12" sm="12" md="12">
      <h1 v-if="isNew" class="h1">Crear camion</h1>
      <h1 v-else class="h1">Modificar camion</h1>
    </v-col>
    <vCol>
      <form @submit.prevent="submitForm()">
        <v-text-field
          id="modelo"
          v-model="vehiculo.modelo"
          name="modelo"
          label="Modelo"
        ></v-text-field>
        <v-text-field
          id="marca"
          v-model="vehiculo.marca"
          name="marca"
          label="Marca"
        ></v-text-field>
        <v-text-field
          id="placa"
          v-model="vehiculo.placa"
          name="placa"
          label="Placa"
        ></v-text-field>
        <v-text-field
          id="kilometraje"
          v-model="vehiculo.kilometraje"
          name="kilometraje"
          label="Kilometraje"
        ></v-text-field>
        <v-text-field
          id="record_servicio"
          v-model="vehiculo.record_servicio"
          name="record_servicio"
          label="Record servicio"
        ></v-text-field>
        <v-switch
          v-model="vehiculo.estado"
          flat
          :label="`Estado: ${vehiculo.estado ? 'Activo' : 'Inactivo'}`"
        ></v-switch>
        <vCol class="d-flex justify-center">
            <vBtn type="submit" color="primary">Guardar</vBtn>
            <vBtn to="/camion" type="button">Cancelar</vBtn>
          </vCol>
      </form>
    </vCol>
  </v-row>
</template>

<script>
export default {
  async asyncData({ params, $axios }) {
    if (params.id) {
      const { vehiculo } = await $axios.$get(`/vehiculo/${params.id}`)
      return { vehiculo }
    }
  },
  data() {
    return {
      vehiculo: {
        modelo: '',
        marca: '',
        placa: '',
        kilometraje: '',
        record_servicio: '',
        estado: true
      },
    }
  },
  computed: {
    isNew() {
      return !this.Id()
    },
  },
  methods: {
    async submitForm() {
      const id = this.Id();
      let response
      if (id) {
        response = await this.$axios.$put(`/vehiculo/${id}`, this.vehiculo);
      } else {
        response = await this.$axios.post('/vehiculo', this.vehiculo);
      }

      if (response) {
        this.$router.push('/camion')
      }
    },
    Id() {
      return this.$route.params.id
    }
  }
}
</script>