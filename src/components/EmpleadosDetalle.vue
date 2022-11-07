<template>
    <div>
        <h1>Empleados detalle</h1>
        <form method="post" style="width: 500px;display: inline-block"
                v-on:submit.prevent="buscarEmpleado">
            <label>Seleccione un empleado</label>
            <select class="form-control" v-model="idEmpleado">
                <option v-for="emp in empleados" 
                    :key="emp.idEmpleado"
                    :value="emp.idEmpleado">
                    {{emp.apellido}}    
                </option>
            </select><br/>
            <button class="btn btn-success">
                Detalles empleado
            </button>
        </form>
        <hr/>
        <div v-if="empleado">
            <h2 style="color:blue">Apellido: {{empleado.apellido}}</h2>
            <dl>
                <dt>Oficio: </dt>
                <dd>{{empleado.oficio}}</dd>
                <dt>Salario: </dt>
                <dd>{{empleado.salario}}</dd>
                <dt>Departamento: </dt>
                <dd>{{empleado.departamento}}</dd>
            </dl>
        </div>
    </div>
</template>

<script>
    import Global from "./../Global";
    import axios from 'axios';

    export default{
        name: "EmpleadosDetalle",
        methods: {
            buscarEmpleado() {
                var request = "/api/empleados/" + this.idEmpleado;
                var url = Global.urlempleados + request;
                axios.get(url).then(response => {
                    this.empleado = response.data
                });
            }
        },
        data() {
            return {
                empleados: [],
                idEmpleado: 0,
                empleado: null
            }
        }, mounted() {
            var request = "/api/empleados";
            var url = Global.urlempleados + request;
            axios.get(url).then(response => {
                this.empleados = response.data
            });
        }
    }
</script>