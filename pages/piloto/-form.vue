<template>
  <v-row justify="center" align="center">
    <v-col class="d-flex justify-space-between" cols="12" sm="12" md="12">
      <h1 v-if="isNew" class="h1">Crear Pilotos</h1>
      <h1 v-else class="h1">Modificar Pilotos</h1>
    </v-col>
    <vCol>
      <form @submit.prevent="submitForm()">
        <v-text-field
          id="nombre"
          v-model="piloto.nombre"
          name="nombre"
          label="Nombre"
        ></v-text-field>
        <v-text-field
          id="dpi"
          v-model="piloto.dpi"
          name="dpi"
          label="DPI"
        ></v-text-field>
        <v-text-field
          id="licencia"
          v-model="piloto.licencia"
          name="licencia"
          label="Licencia"
        ></v-text-field>
        <v-text-field
          id="telefono"
          v-model="piloto.telefono"
          name="telefono"
          label="Telefono"
        ></v-text-field>
        <vCol class="d-flex justify-center">
          <vBtn type="submit" color="primary">Guardar</vBtn>
          <vBtn to="/piloto" type="button">Cancelar</vBtn>
        </vCol>
      </form>
    </vCol>
  </v-row>
</template>

<script>
export default {
  async asyncData({ params, $axios }) {
    if (params.id) {
      const { piloto } = await $axios.$get(`/piloto/${params.id}`)
      return { piloto }
    }
  },
  data() {
    return {
      piloto: {
        nombre: '',
        dpi: '',
        licencia: '',
        telefono: '',
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
      const id = this.Id()
      let response
      if (id) {
        response = await this.$axios.$put(`/piloto/${id}`, this.piloto)
      } else {
        response = await this.$axios.post('/piloto', this.piloto)
      }

      if (response) {
        this.$router.push('/piloto')
      }
    },
    Id() {
      return this.$route.params.id
    },
  },
}
</script>