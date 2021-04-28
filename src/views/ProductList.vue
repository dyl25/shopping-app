<template>
    <h2 class="is-size-3 px-4">Liste des Produits</h2>

    <button @click="displayBasket" class="button is-link"><i class="fas fa-shopping-basket mr-3"></i> Mon Panier ({{ userBasket.total }} €)</button>

    <modal @close-modal="closeModalBasket" :data-visible="showModalBasket">
        <basket-modal-content v-if="userBasket" :data-basket="userBasket" />
    </modal>

    <modal @close-modal="closeModal" :data-visible="showModal">
        <add-product-confirm v-if="selectedProduct" :product="selectedProduct" />
    </modal>

    <div class="columns is-multiline">
        <div v-for="product in products" :key="product.id" class="column is-3">
            <product @add-product="addToBasket" :product="product" />
        </div>
    </div>
</template>

<script>
import axios from "axios"
import Product from "../components/Product.vue"
import Modal from "../components/Modal.vue"
import AddProductConfirm from "../components/AddProductConfirm.vue"
import BasketModalContent from "../components/BasketModalContent"

export default {
    components: {
        'product': Product,
        'modal': Modal,
        'add-product-confirm': AddProductConfirm,
        'basket-modal-content': BasketModalContent
    },
    data() {
        return {
            products: [],
            userBasket: null,
            showModal: false,
            showModalBasket: false,
            selectedProduct: null,
            messages: [],
            errors: [],
        };
    },
    created() {
        this.loadUserBasket();
    },

    mounted() {
        this.loadProdcuts();
    },

    methods: {
        async loadProdcuts() {
            
            await axios.get("http://localhost:3000/products")
            .then(({ data }) => {
                this.products = data
            })
            .catch(err => this.errors.push("Une erreur s'est produite avec les produits:" + err));
        },

        async loadUserBasket() {
            await axios.get("http://localhost:3000/baskets/1")
            .then(({ data }) => {
                console.log(data);
                this.userBasket = data
            })
            .catch(err => this.errors.push("Une erreur s'est produite avec les paniers:" + err));
        },

        addToBasket(productId) {
            this.selectedProduct = this.products.find(prod => prod.id === productId)
            this.showModal = true
        },

        closeModal() {
            this.showModal = false
        },

        closeModalBasket() {
            this.showModalBasket = false
        },

        displayBasket() {
            this.showModalBasket = true
        }

    },
};
</script>