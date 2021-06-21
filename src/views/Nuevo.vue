<template>
<div>
    <Header/>
    <div class="container">
        <form class="izquierda">
            <b-button class="button" type="submit" variant="secondary" 
                @click="salir()">Salir</b-button>
            <div class="row">
                <div class="col-4">
                <input type="text" class="form-control" v-model="form.nombre"
                placeholder="nombre">
                </div>
                <div class="col-4">
                <input type="text" class="form-control" v-model="form.dni"
                placeholder="dni">
                </div>
                <div class="col-4">
                <input type="text" class="form-control" v-model="form.genero"
                placeholder="genero">
                </div>
                <div class="col-8">
                <input type="text" class="form-control" v-model="form.direccion"
                placeholder="direccion">
                </div>
                <div class="col-4">
                <input type="text" class="form-control" v-model="form.codigoPostal"
                placeholder="codigo postal">
                </div>
                <div class="col-4">
                <input type="text" class="form-control" v-model="form.fechaNacimiento"
                placeholder="fecha nacimiento">
                </div>
                <div class="col-4">
                <input type="text" class="form-control" v-model="form.correo"
                placeholder="correo">
                </div>
                <div class="col-4">
                <input type="text" class="form-control" v-model="form.telefono"
                placeholder="Telfono">
                </div>
                <div class="izquierda">
                    <button class="btn btn-success" type="button"
                        @click="guardar()">Agregar 
                    </button>
                </div>
            </div>
        </form>
    </div>
</div>
</template>

<script>
import Header from '@/components/Header'
import axios from 'axios';

export default {
    name:'Nuevo',
    components:{
        Header
    },
    data(){
        return{
            form: {
                "nombre" : "",
                "dni" : "", 
                "correo": "",
                "codigoPostal" : "",
                "direccion" : "",
                "genero" : "",
                "telefono" : "",
                "fechaNacimiento" : "",
                "token" :  ""
            },
            counter: 0
        }
    },
    methods:{
        guardar(){
            console.log(this.form)
            console.log(this.form.token)
            this.form.token = localStorage.getItem("token")
            axios.post("https://solodata.es/pacientes", this.form)
            .then(response => {
                console.log(response)
                this.$router.push('/dashboard')
            })
            .catch(error => {
                console.log(error)
            })
        },

        //async guardar(){
            // this.form.token = localStorage.getItem("token")
            // this.form = [...this.form, this.form.token]
            // const res = await fetch("https://api.solodata.es/pacientes", {
            //     method: 'POST',
            //     headers:{
            //     'Content-type': 'application/json'
            //     },
            //     body: JSON.stringify(this.form)
            // })
            // const data = await res.json()
            // console.log(this.form)
            // console.log('el res' + res)
            // console.log('el data' + data)
        //},
        salir(){
            this.$router.push('/dashboard')
        },
        toast(toaster, append = false) {
        this.counter++
        this.$bvToast.toast(`Toast ${this.counter} body content`, {
          title: `Toaster ${toaster}`,
          toaster: toaster,
          solid: true,
          appendToast: append
        })
      }
    }
}
</script>

<style scoped>
    .form-control{
        margin: 15px 5px;
    }

    .izquierda{
        text-align: right;
    }
</style>

