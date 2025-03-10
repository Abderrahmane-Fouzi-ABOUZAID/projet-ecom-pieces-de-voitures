<template>
    <div class="cart">
        <h3>🛒 My Cart</h3>
        <ul>
            <li v-for="item in cart" :key="item.id">
                {{ item.nom }} - {{ item.prix }} MAD
                <button @click="removeFromCart(index)">Remove</button>
            </li>
        </ul>
        <p v-if="!cart.length">Le panier est vide.</p>
        <p v-else>Total : {{ cartTotal }} MAD</p>
    </div>
</template>

<script setup>
import { defineProps, computed } from 'vue';

const props = defineProps({
  cart: Array,
});

const emit = defineEmits(['remove-from-cart']);

const removeFromCart = (index) => {
  emit('remove-from-cart', index);
};

const cartTotal = computed(() => 
  props.cart.reduce((total, piece) => total + piece.prix, 0)
);
</script>

<style scoped>
.cart {
    font-size: large;
margin-top: 200px;
  margin-left: 10px;
  width: 90%;
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 8px;
}

.cart h3 {
  margin: 0;
  font-size: 1.2em;
}

.cart ul {
  list-style: none;
  padding: 0;
}

.cart li {
  margin-bottom: 5px;
}

button{
    height: 25px;
    width: 70px;
    font-size: medium;
    background-color: red;
    border-radius: 6px;
    border: none;
    margin-left: 5px;
}
</style>
