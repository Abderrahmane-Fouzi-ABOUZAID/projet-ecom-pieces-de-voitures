<template>
    <section class="fiches main">

        <div class="piece-item" v-for="piece in pieces" :key="piece.id">
            <img 
                :src="piece.Image" 
            /><br>
            <span>Product : </span>{{piece.nom}}<br>
            <span>Price : </span>{{piece.prix}}
            <br>
            <button @click="addToCart(piece)">Add to cart</button>
            <br><br>
        </div>
    </section>
</template>

<script setup>
import { defineProps } from 'vue'; 

const props = defineProps({
    pieces: Array,
})

const emit = defineEmits(['add-to-cart']);

const addToCart = (piece) => {
  emit('add-to-cart', piece);
};
</script>


<style scoped>
.main{
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    gap: 10px;

}
.piece-item{
    flex: 1 1 48%;
    font-size: large;
    width: 50%;
}
.piece-item span{
    font-weight: bold;
    color: red;
} 
.piece-item img{
    height: 150px;
    width: 200px;
}
.piece-item button {
    font-size: large;
    width: 200px;
    height: 38px;
  margin-top: 10px;
  padding: 5px 10px;
  background-color: #28a745;
  color: white;
  border: none;
  cursor: pointer;
    border-radius: 6px;
}

.piece-item button:hover {
  background-color: #218838;
}

</style>
