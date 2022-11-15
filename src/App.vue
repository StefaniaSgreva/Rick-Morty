<template>
   <AppHeader title="Rick and Morty App"/>
   <main>
        <AppSearch @filterchar= "getCharacters"/>
        <CharacterList />
        <div v-if="store.errormessage">
            <h1>Opps ! Qualcosa è andato storto</h1>
            <p>{{store.errormessage}}</p>
        </div>
        <ResultCount/>
   </main>
</template>

<script>
    import axios from 'axios';
    import AppHeader from './components/AppHeader.vue';
    import AppSearch from './components/AppSearch.vue';
    import CharacterList from './components/CharacterList.vue';
    import ResultCount from './components/ResultCount.vue';

    import {store} from './store';

    export default {
        components:{
                AppHeader,
                AppSearch,
                CharacterList,
                ResultCount
        },
        data(){
            return{
                store,
                endPoint: 'character',
            }
        },
        // watc:{

        // },
        methods:{
            getCharacters(){ 
                store.errormessage = '';
                // const apiurl = (status) ? this.apiURL + '?status=' + status : this.apiURL;
                let options = null
                if(store.search.status && store.search.name){
                    options = {
                        params:{
                            status: store.search.status, //chiave: valore
                            name: store.search.name,
                        }
                    }
                } else if(store.search.status){
                    options = {
                        params:{
                            status: store.search.status, 
                        }
                    }
                } else if(store.search.name){
                    options = {
                        params:{
                            name: store.search.name,
                        }
                    }
                }
                    
                store.loading= true;
                const apiurl = store.apiURL + this.endPoint;
                axios.get(apiurl, options).then(
                    (res)=>{
                        store.characterList = res.data.results;
                        // console.log(this.characterList);
                        store.loading = false;
                    }
                ).catch((error)=>{
                    store.characterList.lenght = 0;
                    store.loading = false;
                    store.errormessage = error.message;
                    // console.log(error.message);
                    // console.log(error.response.status);
                })
            }
        },
        created(){
            this.getCharacters();
        }
    }
</script>

<style lang="scss" scoped>
    
</style>