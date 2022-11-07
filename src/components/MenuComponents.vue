<template>
  <div>
    <nav class="navbar navbar-expand-lg bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Navbar</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
                <router-link to="/" class="nav-link active">Home</router-link>
            </li>
            <li class="nav-item">
                <router-link to="/coches" class="nav-link">Coches</router-link>
            </li>
            <li class="nav-item">
                <router-link to="/empleadosdetalle" 
                class="nav-link">Empleados detalle</router-link>
            </li>            
            <li class="nav-item dropdown">
              <a
                class="nav-link dropdown-toggle"
                href="#"
                role="button"
                data-bs-toggle="dropdown"
                aria-expanded="false"
              >
                Oficios
              </a>
              <ul class="dropdown-menu">
                <li v-for="oficio in oficios" :key="oficio">
                    <router-link 
                    :to="'/empleadosoficio/' + oficio"
                    class="dropdown-item">
                        {{oficio}}
                    </router-link>
                </li>
              </ul>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
import Global from './../Global';
import axios from 'axios';
export default {
  name: "MenuComponents",
  data() {
    return {
        oficios: []
    }
  }, mounted() {
    var request = "/api/empleados/oficios";
    var url = Global.urlempleados + request;
    axios.get(url).then(response => {
        this.oficios = response.data
    });
  }
};
</script>