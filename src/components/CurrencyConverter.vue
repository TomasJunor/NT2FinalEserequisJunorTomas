<template>
  <section>
    <div>
      <h1>Conversor a Dolares</h1>
      <span>Ingrese monto $ </span> <input type="text" v-model="valorPesos" />
      <br />
      <br />
      <span>Valor del dolar en $ </span>
      <input type="text" v-model="valorDolar" /><span> - Actualizacion </span>
      <input
        type="Checkbox"
        @click="actualizarCotizacion()"
        v-model="valorDolar"
      />
      <span v-if="checked">{{ getDate() }}</span>
      <h4>Valor Convertido USD {{ valorPesos / valorDolar || 0 }}</h4>

<br>
      <h3>Multiple Choice</h3>
      <h5>1 : C</h5>
      <h5>2 : B</h5>
      <h5>3 : C</h5>
      <h5>4 : A</h5>
      <h5>5 : B y C</h5>
    </div>
  </section>
</template>

<script>
export default {
  name: "src-components-CurrencyConverter",
  props: [],
  mounted() {},
  data() {
    return {
      apiCotizaciones:
        "https://www.dolarsi.com/api/api.php?type=valoresprincipales",
      valorPesos: 0,
      valorDolar: 0,
      checked: false,
      interval: null,
    };
  },
  methods: {
    async getCotizacion() {
      try {
        let resp = await this.axios(this.apiCotizaciones);
        let datos = resp.data;
        this.valorDolar = datos
          .find(this.isDolarBlue)
          .casa.venta.replace(",", ".");
      } catch (error) {
        console.error("Error");
      }
    },
    isDolarBlue(e) {
      return e.casa.nombre == "Dolar Blue";
    },
    getDate() {
      return new Date().toLocaleString();
    },
    actualizarCotizacion() {
      this.checked = !this.checked;
      if (this.checked) {
        this.interval = window.setInterval(this.getCotizacion, 2000);
      } else {
        clearInterval(this.interval);
      }
    },
  },
  computed: {},
};
</script>
