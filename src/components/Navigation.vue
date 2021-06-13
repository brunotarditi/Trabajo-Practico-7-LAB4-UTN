<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="dark" fixed="top">
      <b-navbar-brand href="/">Home</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="/dondeEstamos">Donde Estamos</b-nav-item>
          <li class="nav-item">
            <router-link to="/productos" class="nav-link">Productos</router-link>
          </li>
        </b-navbar-nav>

        <b-navbar-nav class="ml-auto">
          <b-nav-form @keyup="busqueda">
            <b-form-input
              size="sm"
              class="mr-sm-2"
              placeholder="Buscar"
              v-model="form.buscar"
            ></b-form-input>
          </b-nav-form>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        buscar: "",
      }
    }
  },
  methods: {
    busqueda() {
      this.$router.push('/productos/'+ this.form.buscar)
    }
  }
};
</script>

<style lang=""></style>
