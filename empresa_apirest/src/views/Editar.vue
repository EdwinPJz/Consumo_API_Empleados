<template>
    <div>
        <Header/>
            <div class="container">
                <form class="form-horizontal">
                    <div class="form-group left">
                        <label class="control-label col-sm-2">Codigo</label>
                        <div class="col-sm-10">
                            <input type="text" class="form-control" name="codigo" id="codigo" placeholder="E001" v-model="form.codigo">
                        </div>
                        
                        <label class="control-label col-sm-2">Nombres</label>
                        <div class="col-sm-10">
                            <input type="text" class="form-control" name="nombres" id="nombres" placeholder="Nombre1 Nombre2" v-model="form.nombres">
                        </div>
                        
                        <label class="control-label col-sm-2">Apellidos</label>
                        <div class="col-sm-10">
                            <input type="text" class="form-control" name="apellidos" id="apellidos" placeholder="Apellido1 Apellidos2" v-model="form.apellidos">
                        </div>
                        
                        <label class="control-label col-sm-2">Dirección</label>
                        <div class="col-sm-10">
                            <input type="text" class="form-control" name="direccion" id="direccion" placeholder="Casa#000 Zona 0, Municipio, Departamento" v-model="form.direccion">
                        </div>
                        
                        <label class="control-label col-sm-2">Teléfono</label>
                        <div class="col-sm-10">
                            <input type="text" class="form-control" name="telefono" id="telefono" placeholder="99999999" v-model="form.telefono">
                        </div>
                        
                        <label class="control-label col-sm-2">Fecha Nacimiento</label>
                        <div class="col-sm-10">
                            <input type="text" class="form-control" name="fecha_nacimiento" id="fecha_nacimiento" placeholder="" v-model="form.fecha_nacimiento">
                        </div>
                    
                        <label class="control-label col-sm-2">Puesto</label>
                        <div class="col-sm-10">
                            <input type="text" class="form-control" name="puesto" id="puesto" placeholder="99999999" v-model="form.id_puesto">
                        </div>
                    </div> 
                    <br />
                    <div class="form-grup">
                        <button type="button" class="btn btn-primary" v-on:click="editar">Editar</button>
                        <button type="button" class="btn btn-danger margen" v-on:click="eliminar()">Eliminar</button>
                        <button type="button" class="btn btn-dark margen" v-on:click="salir()">Salir</button>
                    </div>
                    
                </form>
            </div>
        <Footer/>
    </div>
</template>

<script>
    import Header from '@/components/Header.vue';
    import Footer from '@/components/Footer.vue';
    import axios from 'axios';
    export default{
        name: "Editar",
        components:{
            Header,
            Footer  
        },
        data:function(){
            return{
                form:{
                    "id_empleado": "",
                    "codigo" : "",
                    "nombres" : "",
                    "apellidos" : "",
                    "direccion" : "",
                    "telefono" : "",
                    "fecha_nacimiento" : "",
                    "id_puesto" : ""
                }
            }
        },
        methods:{
            editar(){
                axios.put("https://localhost:5001/api/employee",this.form)
                .then( data => {
                    console.log(data);
                })
            },
            salir(){
                this.$router.push("/");
            },
            eliminar(){
                var enviar = {
                    "id_empleado" : this.form.id_empleado
                };
                axios.delete("https://localhost:5001/api/employee", { headers:enviar })
                .then( datos => {
                    console.log(datos);
                    this.$router.push("/");
                });
            }
        },
        mounted:function(){
            this.form.id_empleado = this.$route.params.id;
            axios.get("https://localhost:5001/api/employee/"+ this.form.id_empleado)
            .then(datos =>{
                
                this.form.codigo = datos.data.codigo;
                this.form.nombres = datos.data.nombres;
                this.form.apellidos = datos.data.apellidos;
                this.form.direccion = datos.data.direccion;
                this.form.telefono = datos.data.telefono;
                this.form.fecha_nacimiento = datos.data.fecha_nacimiento;
                this.form.id_puesto = datos.data.id_puesto;
                console.log(this.form);
            })
        }
    }
</script>

<style>
    .left{
        text-align: left;  
        font-weight:bold;  
    }
</style>