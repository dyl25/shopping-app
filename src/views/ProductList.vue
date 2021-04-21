<template>
    <h2 class="is-size-3 px-4">Liste des Produits</h2>

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

export default {
    components: {
        'product': Product,
        'modal': Modal,
        'add-product-confirm': AddProductConfirm
    },
    data() {
        return {
            products: [],
            userBasket: null,
            showModal: false,
            selectedProduct: null,
            messages: [],
            errors: [],
        };
    },

    mounted() {
        this.loadProdcuts()
        this.loadUserBasket()
    },

    methods: {
        loadProdcuts() {
            
            axios.get("http://localhost:3000/products")
            .then(({ data }) => {
                this.products = data;
            })
            .catch(err => this.errors.push("Une erreur s'est produite avec les produits:" + err));
        },

        loadUserBasket() {
            axios.get("http://localhost:3000/basket")
            .then(({ data }) => {
                this.userBasket = data[0]
            })
            .catch(err => this.errors.push("Une erreur s'est produite avec les paniers:" + err));
        },

        addToBasket(productId) {
            console.log(productId);
            this.selectedProduct = this.products.find(prod => prod.id === productId)
            this.showModal = true
        },

        closeModal() {
            this.showModal = false
        }

    },
};
</script>