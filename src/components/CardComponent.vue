<template>
   <div class="character">
        <img :src="character.image" :alt="character.name">
        <h1>{{character.name}}</h1>
        <h2>{{character.status}}</h2>
        <h3>{{character.species}}</h3>
    </div>
</template>

<script>
    export default {
        props:{
            character: Object
        }
    }
</script>

<style lang="scss" scoped>

</style>