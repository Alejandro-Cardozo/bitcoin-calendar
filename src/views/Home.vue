<template>
  <div>
    <v-layout :wrap="true">
      <v-flex xs12>
        <v-card>
          <v-date-picker
            v-model="fecha"
            full-width
            locale="es-ar"
            :min="min"
            :max="max"
            @change="getBitcoin(fecha)"
          >
          </v-date-picker>
        </v-card>
        <v-card color="primary" dark>
          <v-card-text align="center" class="display-1">
            {{ valor }}
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      fecha: new Date().toISOString().substr(0, 10),
      min: "2009",
      max: new Date().toISOString().substr(0, 10),
      valor: null
    };
  },
  methods: {
    async getBitcoin(dia) {
      let arrayFecha = dia.split(["-"]);
      let ddmmyyyy = arrayFecha[2] + "-" + arrayFecha[1] + "-" + arrayFecha[0];
      console.log(ddmmyyyy);

      try {
        let datos = await axios.get(
          `https://mindicador.cl/api/bitcoin/${ddmmyyyy}`
        );
        console.log(datos.data);
        if (datos.data.serie.length > 0) {
          this.valor = await datos.data.serie[0].valor;
        } else {
          this.valor = "Sin resultados";
        }
        this.valor = await datos.data.serie[0].valor;
      } catch (error) {
        console.log(error);
      } finally {
      }
    }
  },
  created() {
    this.getBitcoin(this.fecha);
  }
};
</script>
