<template>
    <div class="header">
    <b-navbar type="dark" variant="dark">
        <b-navbar-nav>
        <b-nav-item @click="goHome()">Home</b-nav-item>

        <b-nav-item @click="agregar()">Agregar</b-nav-item>

        <b-nav-item-dropdown text="User" right>
            <b-dropdown-item href="#">Account</b-dropdown-item>
        
        <b-dropdown-item href="#">Settings</b-dropdown-item>
        </b-nav-item-dropdown>
        </b-navbar-nav>
    </b-navbar>
    </div>
</template>

<script>
export default {
    name: 'Header',
    methods:{
        agregar(){
            this.$router.push("/nuevo")
        },
        goHome(){
            this.$router.push('/dashboard')
        }
    }
}
</script>

<style scoped>

    .header{
        margin-bottom: 50px;
    }
    
</style>