<template>
  <div>
    <v-layout :wrap="true">
      <v-flex xs12>
        <v-card>
          <v-date-picker v-model="fecha" full-width> </v-date-picker>
        </v-card>
        <v-card color="primary" dark>
          <v-card-text align="center" class="display-1">
            Hola mundo el dia {{ fecha }}
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
export default {
  data() {
    return {
      fecha: ""
    };
  }
};
</script>
