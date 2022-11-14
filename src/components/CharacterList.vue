<template>
    <div class="container">
        <div class="loading" v-if="loading">Sto caricando i dati</div>
        <div class="row" v-if="!loading">
            <div class="col-12 col-sm-6 col-md-4 col-lg-3">
                <div class="character" v-for="(item,index) in characters" :key="item.id">
                    <img :src="item.image" :alt="item.name">
                    <h1>{{item.name}}</h1>
                    <h2>{{item.status}}</h2>
                    <h3>{{item.species}}</h3>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'CharacterList',
        props: ['characters', 'loading']
    }
</script>

<style lang="scss" scoped>

</style>