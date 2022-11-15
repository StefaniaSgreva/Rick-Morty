<template>
   <AppHeader title="Rick and Morty App"/>
   <main>
        <AppSearch @filterchar= "getCharacters"/>
        <CharacterList :characters="characterList"
        :loading="loading"/>
        <div v-if="errormessage">
            <h1>Opps ! Qualcosa è andato storto</h1>
            <p>{{errormessage}}</p>
        </div>
   </main>
</template>

<script>
    import axios from 'axios';
    import AppHeader from './components/AppHeader.vue'
    import AppSearch from './components/AppSearch.vue'
    import CharacterList from './components/CharacterList.vue'
    export default {
        components:{
            AppHeader,
            AppSearch,
            CharacterList
        },
        data(){
            return{
                apiURL: 'https://rickandmortyapi.com/api/character',
                characterList: [],
                loading: false,
                searchStatus: '',
                errormessage: '',
            }
        },
        methods:{
            getCharacters(status){ 
                this.errormessage = '';
                // const apiurl = (status) ? this.apiURL + '?status=' + status : this.apiURL;
                let options = null
                if(status){
                    options = {
                        params:{
                            status: status, //chiave: valore
                        }
                    }
                };
                    
                this.loading= true;
                axios.get(this.apiURL, options).then(
                    (res)=>{
                        this.characterList = [...res.data.results];
                        console.log(this.characterList);
                        this.loading = false;
                    }
                ).catch((error)=>{
                        this.loading = false;
                        this.errormessage = error.message;
                        console.log(error.message);
                        console.log(error.response.status);
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