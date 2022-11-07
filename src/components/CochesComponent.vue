<template>
    <div>
        <h1>Api Coches</h1>
        <div class="card" v-for="car in coches" :key="car.idcoche">
            <h1 style="color:blue">
                {{car.marca}}, {{car.modelo}}
            </h1>
            <h2 style="color:red"> {{car.conductor}} </h2>
            <img :src="car.imagen" style="width: 150px; height: 150px"/>
        </div>
    </div>
</template>

<script>
    //NECESITAMOS IMPORTAR GLOBAL
    import Global from './../Global';
    //NECESITAMOS IMPORTAR axios
    import axios from 'axios';

    export default {
        name: "CochesComponent"
        , data() {
            return {
                coches: []
            }
        }, methods: {
            loadCoches() {
                var request = "/webresources/coches";
                var url = Global.urlcoches + request;
                axios.get(url).then(response => {
                    this.coches = response.data;
                });
            }
        }, mounted() {
            this.loadCoches();
        }
    }
</script>