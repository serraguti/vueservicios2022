<template>
    <div>
        <h1>Empleados Oficio</h1>
        <table class="table table-bordered">
            <thead>
                <tr>
                    <th>APELLIDO</th>
                    <th>OFICIO</th>
                    <th>SALARIO</th>
                    <th>DEPARTAMENTO</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="empleado in empleados" :key="empleado.idEmpleado">
                    <td>{{empleado.apellido}}</td>
                    <td>{{empleado.oficio}}</td>
                    <td>{{empleado.salario}}</td>
                    <td>{{empleado.departamento}}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
import Global from './../Global';
import axios from 'axios';

    export default{
        name: "EmpleadosOficio",
        data() {
            return {
                empleados: []
            }
        },
        watch: {
            '$route.params.oficio'(nextVal, prevVal){
                if (nextVal != prevVal){
                    this.loadEmpleados();
                }
            }
        },
        methods: {
            loadEmpleados() {
                var oficio = this.$route.params.oficio;
                var request = "/api/empleados/empleadosoficio/" + oficio;
                var url = Global.urlempleados + request;
                axios.get(url).then(response => {
                    this.empleados = response.data
                });
            }
        }, mounted() {
            this.loadEmpleados();
        }
    }
</script>