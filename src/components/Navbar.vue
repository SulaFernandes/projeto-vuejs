<template>
    <div id="nav">
        
        <router-link to="/" id="logo-url"><img :src="logo" :alt="alt" id="logo"></router-link>
        <router-link to="/">Home</router-link> 
        <router-link to="/listar">Listar</router-link>
        
    </div>
    
</template>
<script>
export default {
    name: 'Navbar',
    props: ['logo', 'alt']

}
</script>
<style scoped>
    #nav {
        background-color: #222;
        border-bottom: 4px solid #d225f5;
        padding: 5px 20px;
        display: flex;
        justify-content: flex-end;
        align-items: center;

    }
    #nav #logo-url {
        margin: auto;
        margin-left: 0;
    }
    #logo {
        width: 30px;
        height: 30px;
    }
    #nav a {
        color: #FFF;
        text-decoration: none;
        margin: 12px;
        transition: .5s;
        font-weight: bold;
    }
    #nav a:hover {
        color: #d225f5;
        
    }

</style>
