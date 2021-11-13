<template>
  <v-row justify="center" align="center">
    <v-col class="d-flex justify-space-between" cols="12" sm="12" md="12">
      <h1 class="h1">Pilotos</h1>
      <v-btn color="primary">Crear</v-btn>
    </v-col>
    <vCol>
      <form>
        <v-text-field id="nombre" v-model="piloto.nombre" name="nombre" label="Nombre"></v-text-field>
        <v-text-field id="dpi" v-model="piloto.dpi" name="dpi" label="DPI"></v-text-field>
        <v-text-field id="licencia" v-model="piloto.licencia" name="licencia" label="Licencia"></v-text-field>
        <v-text-field id="telefono" v-model="piloto.telefono" name="telefono" label="Telefono"></v-text-field>
      </form>
    </vCol>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
        piloto: {
            nombre: '',
            dpi: '',
            licencia: '',
            telefono: ''
        }
    }
  },
}
</script>