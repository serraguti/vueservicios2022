<template>
    <div>
        <h1>Home Servicios VUE</h1>
        <h1 style="color:blue">
            {{saludo}}
        </h1>
    </div>
</template>

<script>
import ServiceEjemplo from './../services/ServiceEjemplo';
//PARA PODER UTILIZAR NUESTRO SERVICIO, DEBEMOS INSTANCIAR
//UN OBJETO DE LA CLASE EN EL COMPONENT
const service = new ServiceEjemplo();

    export default {
        name: "HomeComponent", 
        data() {
            return {
                saludo: ""
            }
        }, 
        mounted() {
            this.saludo = service.getSaludo("Alumno");
        }
    }
</script>