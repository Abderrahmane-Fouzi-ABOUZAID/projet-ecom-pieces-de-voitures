<template>
    <div class="main">
        <section class="filtres">
            <h3>Filtres</h3>
            <p>Category : </p>
            <select @change="handleCategoryChange" v-model="SelectedCategory">
                <option value="default" selected>Select a category</option>
                <option v-for="(category, index) in categories" :value="category" :key="index">{{category}}</option>
            </select><br><br>
            <p>Search bar : </p>
            <input v-model="liveSearch" @input="handleLiveText">
            <p>Disponibility : </p>
            <select @change="handleDispoChange" v-model="SelectedDispo">
                <option value="default" selected>Select a disponibility</option>
                <option v-for="(dispo, index) in dispos" :value="dispo" :key="index">{{dispo}}</option>
            </select>
        </section>
    </div>
</template>


<script setup>
import { ref } from 'vue';
import { defineEmits } from 'vue';

const emit = defineEmits(['selected-category', "live-search", "selected-dispo"]);

const liveSearch = ref("");

const SelectedCategory = ref("default");

const SelectedDispo = ref("default");

const props = defineProps({
    categories: Array,
    dispos: Array
})

const handleLiveText = () => {
    emit("live-search", liveSearch.value);
}

const handleCategoryChange = () => {
    emit("selected-category", SelectedCategory.value);
}

const handleDispoChange = () => {
    emit("selected-dispo", SelectedDispo.value);
}


</script>


<style scoped>
.main{
    display: flex;
    flex-direction: row;
    width: 30%;
    height: 300px;
}

select{
    margin-left: 30px;
    height: 40px;
    width: 240px;
    font-size: large;
}
p{
    font-size: large;
    margin-left: 30px;
}
input{
    font-size: large;
    margin-left: 30px;
    padding: 5px;
}
</style>


