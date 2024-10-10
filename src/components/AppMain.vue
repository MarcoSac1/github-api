<script>
import AppSearch from './AppSearch.vue';
import CardList from './CardList.vue';
import axios from 'axios';
export default{
    components: {
        CardList,
        AppSearch
    },
    data(){
        return{
            tipologiaSelected: null,
            cards:[],
            tipiRicerca: [
                {
                    nome: 'utenti',
                    descrizione: 'Utenti/Organizzazioni'
                },
                {
                    nome: 'repo',
                    descrizione: 'Repository'
                }
            ]
        }
    },
    methods:{
        onTipologiaSelected(tipologia) {
            this.tipologiaSelected = tipologia;
        },
        onQuerySearch(tipologia, query) {
            console.log('tipologia', tipologia)
            console.log('query', query)

            // In base alla tipologia chiamo searchUtenti o searchRepo
        },
        searchUtenti(query){
            axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0&archetype=' + query)
            .then((response) => {
                console.log(response.items);
                this.cards=response.items;
            })
            .catch(function(error){
                console.log(error);
            })
            .finally(function () {
                
            });
        },
        searchRepo(query){
            axios.get('https://db.ygoprodeck.com/api/v7/archetypes.php')
            .then((response) => {
                console.log(response.items);
                this.cards=response.items;
                console.log(this.tipiRicerca);
            })
            .catch(function(error){
                console.log(error);
            })
            .finally(function () {
                
            });
        },

    },
    created(){
    }

}
</script>

<template>
    <main>
        <AppSearch @selected='onTipologiaSelected' @searched="onQuerySearch" :tipiRicerca="tipiRicerca"/>
        <CardList :cards="cards"/>
    </main>
</template>

<style scoped>

</style>
