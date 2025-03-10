<template>
    <Title title="Les bonnes pièces"/><br>
    <div class="product-container">
        <div class="filtre">
            <Filtre :dispos="dispos" :categories="categories" @selected-category="handleSelectedCategory" @selected-dispo="handleSelectedDispo" @live-search="handleLiveSearch"/><br><br><br>

            <Panier :cart="cart" @remove-from-cart="handleRemoveFromCart"/>
        </div>
        <div class=list>
            <PieceList :pieces="filteredPieces" @add-to-cart="handleAddToCart" />
        </div>
    </div>
</template>



<script setup>

import Title from './components/Title.vue'
import Filtre from './components/Filtre.vue'
import PieceList from './components/PieceList.vue';
import Panier from './components/Panier.vue';

import { ref, computed } from 'vue';

const cart = ref([]);

const handleAddToCart = (piece) => {
  cart.value.push(piece);
};

const handleRemoveFromCart = (index) => {
  cart.value.splice(index, 1); 
};

const selectedCategory = ref("default");

const selectedDispo = ref("default");

const liveSearch = ref(null);

const handleSelectedCategory = (category) =>{
    selectedCategory.value = category;
};

const handleSelectedDispo = (dispo) =>{
    selectedDispo.value = dispo
}

const handleLiveSearch = (text) => {
    liveSearch.value = text;
};

const filteredPieces = computed(() => {
    return pieces.filter(piece => {
        const matchesCategory = selectedCategory.value === "default"  || piece.categorie === selectedCategory.value;
        const matchesSearch = !liveSearch.value || piece.nom.toLowerCase().includes(liveSearch.value.toLowerCase());
        const matchesDispo = selectedDispo.value === "default" || (piece.Disponible === true && selectedDispo.value === "Available") || (piece.Disponible === false && selectedDispo.value === "Unavailable");
        return matchesCategory && matchesSearch && matchesDispo;
    });
});



const categories = ['Électricité', 'Filtration', 'Moteur', 'Freinage', 'Refroidissement', 'Sécurité', 'Suspension',
'Transmission', 'Carburant', 'Carrosserie', 'Échappement', 'Direction'];

const dispos = ["Available", "Unavailable"];


const pieces = [
    {
        "id": 1,
        "nom": "Batterie 12V",
        "prix": 120,
        "categorie": "Électricité",
        "Image": "https://www.valeo.com/wp-content/uploads/2023/06/2015_PES_Alternator_Leaders.png",
        "Disponible": true
    },
    {
        "id": 2,
        "nom": "Filtre à huile",
        "prix": 15,
        "categorie": "Filtration",
        "Image": "https://www.bouchrapieces.ma/wp-content/uploads/2023/11/OX1301-D.jpg",
        "Disponible": true
    },
    {
        "id": 3,
        "nom": "Bougies d'allumage (x4)",
        "prix": 35,
        "categorie": "Moteur",
        "Image": "https://img-4.linternaute.com/LeACP-S13-WOYuS7AHrHJQxmrus=/1500x/smart/353cb0927cf84e1186ac9727f953f915/ccmcms-linternaute/10660420.jpg",
        "Disponible": false
    },
    {
        "id": 4,
        "nom": "Disques de frein (x2)",
        "prix": 80,
        "categorie": "Freinage",
        "Image": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQKzKQ9kkF7yZOZhnRNyKrS1mFnua_oAwUwnw&s",
        "Disponible": true
    },
    {
        "id": 5,
        "nom": "Courroie de distribution",
        "prix": 90,
        "categorie": "Moteur",
        "Image": "https://images.ad.fr/1/image/kit-distribution-pompe-a-eau-courroie-accessoire.jpg",
        "Disponible": false
    },
    {
        "id": 6,
        "nom": "Pompe à eau",
        "prix": 70,
        "categorie": "Refroidissement",
        "Image": "https://wordpress-content.vroomly.com/wp-content/uploads/2023/03/fonctionnement_pompe_a_eau.jpg",
        "Disponible": true
    },
    {
        "id": 7,
        "nom": "Amortisseurs arrière (x2)",
        "prix": 150,
        "categorie": "Suspension",
        "Image": "https://leader-moto.com/wp-content/uploads/2022/05/AMORTISSEUR-AR-CG-TVR.png",
        "Disponible": true
    },
    {
        "id": 8,
        "nom": "Filtre à air",
        "prix": 20,
        "categorie": "Filtration",
        "Image": "https://www.gomecano.com/wp-content/uploads/2021/09/filtre-a-air-moteur-gomecano.jpeg",
        "Disponible": true
    },
    {
        "id": 9,
        "nom": "Capteur ABS",
        "prix": 50,
        "categorie": "Sécurité",
        "Image": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcREu7pi0EZUU8JWkfwCaLyHNWTTSgDxWLH2aw&s",
        "Disponible": false
    },
    {
        "id": 10,
        "nom": "Radiateur de refroidissement",
        "prix": 130,
        "categorie": "Refroidissement",
        "Image": "https://assets-valeo.keepeek.com/medias/domain8143/media103031/909376-7vjmv3l3a9-preview1.png",
        "Disponible": true
    },
    {
        "id": 11,
        "nom": "Alternateur",
        "prix": 200,
        "categorie": "Électricité",
        "Image": "https://img-4.linternaute.com/YX50Di0_-jbCH5qpGkXOo5bQNIo=/1500x/smart/640932cb373e44d585b703f5b2479491/ccmcms-linternaute/10653342.jpg",
        "Disponible": true
    },
    {
        "id": 12,
        "nom": "Démarreur",
        "prix": 180,
        "categorie": "Électricité",
        "Image": "https://img-4.linternaute.com/zHBjoHWfKyV2WEYLirk75qkCzzE=/1500x/smart/b8fb43027aa64f459df75373fdc952a7/ccmcms-linternaute/10653930.jpg",
        "Disponible": false
    },
    {
        "id": 13,
        "nom": "Kit d’embrayage",
        "prix": 220,
        "categorie": "Transmission",
        "Image": "https://wordpress-content.vroomly.com/wp-content/uploads/2023/03/iStock-866353964.jpg",
        "Disponible": true
    },
    {
        "id": 14,
        "nom": "Injecteur de carburant",
        "prix": 110,
        "categorie": "Moteur",
        "Image": "https://m.media-amazon.com/images/I/511FOs9cr+L.jpg",
        "Disponible": true
    },
    {
        "id": 15,
        "nom": "Pompe à carburant",
        "prix": 90,
        "categorie": "Carburant",
        "Image": "https://www.ms-motorservice.com/_assets/thumbnail/3107/image?1718878899",
        "Disponible": true
    },
    {
        "id": 16,
        "nom": "Capteur de pression des pneus",
        "prix": 45,
        "categorie": "Sécurité",
        "Image": "https://wordpress-content.vroomly.com/wp-content/uploads/2023/03/thumb.jpg",
        "Disponible": true
    },
    {
        "id": 17,
        "nom": "Rétroviseur extérieur",
        "prix": 60,
        "categorie": "Carrosserie",
        "Image": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTon1nH5vaWtm2oNln5ZbE3FrhDr-rEcj0BPw&s",
        "Disponible": false
    },
    {
        "id": 18,
        "nom": "Échappement complet",
        "prix": 250,
        "categorie": "Échappement",
        "Image": "https://www.driftshop.fr/blog/wp-content/uploads/2021/06/echappement2-full-exhaust-1024x665.jpg",
        "Disponible": true
    },
    {
        "id": 19,
        "nom": "Vanne EGR",
        "prix": 140,
        "categorie": "Moteur",
        "Image": "https://www.points.fr/wp-content/uploads/2023/11/vanne_EGR3-800x600-1.jpg",
        "Disponible": true
    },
    {
        "id": 20,
        "nom": "Turbo",
        "prix": 400,
        "categorie": "Moteur",
        "Image": "https://wordpress-content.vroomly.com/wp-content/uploads/2023/03/iStock-512902562.jpg",
        "Disponible": true
    },
    {
        "id": 21,
        "nom": "Joint de culasse",
        "prix": 75,
        "categorie": "Moteur",
        "Image": "https://www.ecoleauto.com/wp-content/uploads/2017/07/image001-5.jpg",
        "Disponible": false
    },
    {
        "id": 22,
        "nom": "Boîtier de direction",
        "prix": 300,
        "categorie": "Direction",
        "Image": "https://www.microprix.fr/259960-large_default/boitier-de-direction-t2-4-72-4-79-qualite-standard.jpg",
        "Disponible": true
    },
    {
        "id": 23,
        "nom": "Silent bloc de suspension",
        "prix": 35,
        "categorie": "Suspension",
        "Image": "https://wordpress-content.vroomly.com/wp-content/uploads/2023/03/iStock-1143587404.jpg",
        "Disponible": true
    },
    {
        "id": 24,
        "nom": "Cardan de transmission",
        "prix": 160,
        "categorie": "Transmission",
        "Image": "https://dam-static.mister-auto.com/assets/maintenance-tips/fr/cardan_opt-1.png",
        "Disponible": true
    },
    {
        "id": 25,
        "nom": "Capteur de position vilebrequin",
        "prix": 50,
        "categorie": "Moteur",
        "Image": "https://wordpress-content.vroomly.com/wp-content/uploads/2023/03/capeur-pmh.jpg",
        "Disponible": true
    }
]



</script>

<style scoped>
    .product-container{
        display: flex;
        flex-direction: row;
    }    
    .list{
        width: 70%;
        margin-left: 100px;
    }    
    .filtre{
        display: flex;
        flex-direction: column;
        width: 30%;
    }
</style>
