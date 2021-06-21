<template>
<div>
    <Header/>
    <h1>Editar paciente</h1>
    <div class="container izquierda">
        <b-button class="button" type="submit" variant="primary" @click="salir()">Salir</b-button>
        <div class="row">
            <div class="col-4">
            <input type="text" class="form-control" v-model="form.nombre">
            </div>
            <div class="col-4">
            <input type="text" class="form-control" v-model="form.dni">
            </div>
            <div class="col-4">
            <input type="text" class="form-control" v-model="form.genero">
            </div>
            <div class="col-8">
            <input type="text" class="form-control" v-model="form.direccion">
            </div>
            <div class="col-4">
            <input type="text" class="form-control" v-model="form.codigoPostal">
            </div>
            <div class="col-4">
            <input type="text" class="form-control" v-model="form.fechaNacimiento">
            </div>
            <div class="col-4">
            <input type="text" class="form-control" v-model="form.correo">
            </div>
            <div class="izquierda">
                <b-button class="button" type="submit" variant="danger"
                @click="borrar()">Borrar</b-button>
                <b-button class="button" type="button" variant="secondary" 
                @click="editar()">Editar</b-button>
            </div>
        </div>
    </div>
</div>
</template>

<script>
import Header from '@/components/Header'
import axios from 'axios';

export default {
    name:'Editar',
    components:{
        Header
    },
    data(){
        return{
            form: {
                "pacienteId" : "",
                "nombre" : "",
                "dni" : "", 
                "correo":"",
                "codigoPostal" :"",
                "genero" : "",
                "telefono" : "",
                "fechaNacimiento" : "",
                "token" : "" 
            }
        }
    },
    methods:{
        borrar(){
            var enviar = {
                "pacienteId": this.form.pacienteId,
                "token": this.form.token
            }
            axios.delete("https://api.solodata.es/pacientes", { headers: enviar })
                .then(response => {
                    console.log(response)
                this.$router.push('/dashboard')
                })
        },
        editar(){
            axios.put("https://api.solodata.es/pacientes", this.form).then(response => {
                console.log(response)
                this.$toastr.success('Message', 'Notificacion');
            })
        },
        salir(){
            this.$router.push('/dashboard')
        }
    },
    mounted(){
      this.form.pacienteId = this.$route.params.id
      let url = "https://api.solodata.es/pacientes?id=" + this.form.pacienteId
      axios.get(url)
      .then(response => {
          this.form.nombre = response.data[0].Nombre
          this.form.dni = response.data[0].DNI
          this.form.genero = response.data[0].Genero
          this.form.direccion = response.data[0].Direccion
          this.form.codigoPostal = response.data[0].CodigoPostal
          this.form.fechaNacimiento = response.data[0].FechaNacimiento
          this.form.telefono = response.data[0].Telefono
          this.form.correo = response.data[0].Correo
          this.form.token = localStorage.getItem("token")
          console.log(this.form)
      })
    },
}
</script>

<style scoped>

    .form-control{
        margin: 15px 5px;
    }

    .izquierda{
        text-align: right;
    }

    .button{
        margin: 15px;
        width: 20%;
    }
    
</style>