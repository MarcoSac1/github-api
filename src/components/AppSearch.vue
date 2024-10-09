<script>
export default{
    components: {
        
    },
    data(){
        return{
            cercato:'',
            cercatoDesc: 'Tipologia Ricerca',
            queryRicerca: ''
        }
    },
    props:{
        tipiRicerca:{
            type: Array,
            required: true
        }
    }
    
}
</script>

<template >
    
    <section class="container mb-4 mt-4">
        <div class="row">
            <div class="col-md-4">
                <div class="dropdown">
                    <button class="btn btn-danger dropdown-toggle" type="button" data-bs-toggle="dropdown" aria-expanded="false" >
                        {{  cercatoDesc }}
                    </button>
                    <ul class="dropdown-menu dropdown-menu-dark">
                        <li  v-for="(tipiRicerca, index) in tipiRicerca" :key="index" :tipiRicerca="tipiRicerca"  >
                            <a class="dropdown-item " @click="cercato = tipiRicerca.nome;cercatoDesc = tipiRicerca.descrizione"  href="#">{{ tipiRicerca.descrizione }}</a>
                        </li>
                    </ul>
                </div>
            </div>
            <div class="col-md-6" v-if="cercato">
                    <input class="form-control" v-model="queryRicerca" type="search" placeholder="Search" aria-label="Cerca">
            </div>
            <div class="col-md-2" v-if="cercato">
                <button class="btn btn-outline-success" @click="$emit('searched', cercato, queryRicerca)" type="submit">Cerca</button>
            </div>
        </div>
    </section>
</template>
<!-- v-model="cercato"  -->
<style scoped>
    .dropdown-menu {
        max-height: 500px;
        overflow-y: auto;
    }
</style>
