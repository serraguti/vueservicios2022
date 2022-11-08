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
import EmpleadosService from './../services/EmpleadosService';
const service = new EmpleadosService();

    export default{
        name: "EmpleadosDetalle",
        methods: {
            buscarEmpleado() {
                service.findEmpleado(this.idEmpleado).then(result => {
                    this.empleado = result;
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
            service.getEmpleados().then(result => {
                this.empleados = result;
            });
        }
    }
</script>