<template>
  <div style="margin-top:80px">
    <div
      v-for="instrumento in buscarMarca"
      :key="instrumento.id"
      style="margin-top:15px"
      class="d-flex justify-content-center"
    >
      <instrumento-item :instrumentoParam="instrumento"></instrumento-item>
    </div>
  </div>
</template>

<script>
import Instrumento from "@/components/Instrumento.vue";

export default {
  name: "Productos",
  components: {
    "instrumento-item": Instrumento,
  },
  computed: {
    buscarMarca: function() {
      const filtro = this.$route.params.filtro;
      return this.instrumentosData.filter((instrumento) => {
       return instrumento.marca.toLowerCase().indexOf(filtro.toLowerCase()) > -1 || 
       instrumento.modelo.toLowerCase().indexOf(filtro.toLowerCase()) > -1 ||
        instrumento.instrumento.toLowerCase().indexOf(filtro.toLowerCase()) > -1 ;
      });
    },
  },
  mounted() {
    this.getInstrumentos();
  },
  data() {
    return {
      instrumentosData: [],
    };
  },
  methods: {
    async getInstrumentos() {
      await fetch("/instrumentos.json")
        .then((res) => res.json())
        .then((data) => {
          this.instrumentosData = data.instrumentos;
        });
    },
  },
};
</script>
