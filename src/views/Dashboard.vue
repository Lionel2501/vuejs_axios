<template>
<div>
    <Header/>
    <div class="container">
        <table class="table table-dark">
        <thead>
            <tr>
                <th scope="col">ID</th>
                <th scope="col">Nombre</th>
                <th scope="col">DNI</th>
                <th scope="col">Telefono</th>
                <th scope="col">E-mail</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="paciente in listaPaciente" :key="paciente.PacienteId"
            @click="editar(paciente.PacienteId)">
                <th>{{ paciente.PacienteId }}</th>
                <td>{{ paciente.Nombre }}</td>
                <td>{{ paciente.DNI }}</td>
                <td>{{ paciente.Telefono }}</td>
                <td>{{ paciente.Correo }}</td>
            </tr>
        </tbody>
        </table>
    </div>
    <Footer />
</div>
</template>

<script>
import Header from '@/components/Header'
import Footer from '@/components/Footer'
import axios from 'axios';

export default {
    name: 'Dashboard',
    components: {Header, Footer},
    data(){
        return {
            listaPaciente: null,
            pagina: 1
        }
    },
    mounted(){
      let url = "https://api.solodata.es/pacientes?page=" + this.pagina

      axios.get(url)
      .then(response => {
          this.listaPaciente = response.data
      })
    },
    methods:{
        editar(id){
            this.$router.push('/editar/' + id)
        }
    }
}
</script>