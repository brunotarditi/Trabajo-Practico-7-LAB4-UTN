<template>
<div style="margin-top:80px">
    <b-container fluid class="mt-4">
      <b-row>
        <b-col>
          <b-img :src="'/img/' + instrumentoEncontrado.imagen" class="d-block mx-auto sizeImg"></b-img>
          <p class="title">Descripción:</p>
          <p class="descripcion">{{ instrumentoEncontrado.descripcion }}</p>
        </b-col>
        <b-col lg="0">
            <div class="verticalLine d-none d-lg-block"></div>
        </b-col>
        <b-col lg="4">
          <b-row>
            <b-col>
              <span>{{ instrumentoEncontrado.cantidadVendida }} vendidos</span>
            </b-col>
          </b-row>
          <b-row>
            <b-col>
              <p class="instrumento">{{ instrumentoEncontrado.instrumento }}</p>
            </b-col>
          </b-row>
          <b-row>
            <b-col>
              <p>{{ instrumentoEncontrado.precio | currency }}</p>
            </b-col>
          </b-row>
          <b-row>
            <b-col>
              <p class="title">Marca: {{ instrumentoEncontrado.marca }}</p>
              <p class="title">Modelo: {{ instrumentoEncontrado.modelo }}</p>
            </b-col>
          </b-row>
          <b-row class="mt-4">
            <b-col>
              <span v-if="instrumentoEncontrado.costoEnvio == 'G'" class="gratis">
                <b-card-img
                  src="/img/camion.png"
                  style="max-width: 35px;"
                ></b-card-img>
                Envío gratis
              </span>
              <span v-else class="costoEnvio"
                >Costo de envío al interior de Argentina:
                {{ instrumentoEncontrado.costoEnvio | currency }}</span
              >
            </b-col>
          </b-row>
          <b-row class="mt-3 pt-3">
            <b-col>
              <b-button size="sm" variant="outline-info">Agregar al carrito</b-button><br>
              <b-button size="sm" variant="primary" href="/productos">Volver</b-button>
            </b-col>
          </b-row>
        </b-col>
        <b-col lg="1">
            <div class="verticalLine d-none d-lg-block"></div>
        </b-col>
      </b-row>
    </b-container>
</div>
</template>

<script>
export default {
  name: "DetalleInstrumento",
  components: {},
  mounted() {
    this.getInstrumentoPorId();
  },
  data() {
    return {
      instrumentoEncontrado: [],
    };
  },
  methods: {
    async getInstrumentoPorId() {
      const parametroId = this.$route.params.id;
      const res = await fetch("/instrumentos.json");
      const resJson = await res.json();
      console.log(resJson);
      this.instrumentoEncontrado = await resJson.instrumentos.find(
        (instrumento) => instrumento.id === parametroId
      );
      console.log(this.instrumentoEncontrado);
    },
  },
};
</script>
<style scoped>
.title{
  font-size: 16px;
  font-weight: bold;
}

.descripcion{
  font-size: 13px;
}

.instrumento {
  font-size: 24px;
  font-weight: bold;
}
.verticalLine {
  border-left: 1px solid rgba(134, 126, 126, 0.26);
  height: 100%;
}
.gratis {
  color: #00bd4f;
}

.costoEnvio {
  color: #e94d05;
}
.sizeImg {
  min-width: 300px;
  max-width: 300px;
}
</style>
