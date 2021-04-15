<template>
    <h2 class="is-size-3 px-4">Liste des Produits</h2>

    <div class="columns is-multiline">
        <article v-for="product in products" :key="product.id" class="column is-3 px-5 mt-3 hoverable is-clickable">
            <div>
                <h3 class="is-size-4 is-inline-block mr-3">{{ product.name }}</h3>
                <span class="tag is-danger is-light is-inline-block is-medium"
                    >Elite</span
                >
            </div>
            <div>{{ product.description }}</div>
            <div class="tags mt-3 mb-1">
                <span class="tag is-primary is-light">abdos</span>
                <span class="tag is-primary is-light">ventre plat</span>
                <span class="tag is-primary is-light">Three</span>
                <span v-for="tag in product.tags" :key="tag.id">{{ tag.name }}</span>
            </div>
            <div>07-03-2021</div>
        </article>
    </div>
</template>

<script>
import axios from "axios";

export default {
    data() {
        return {
            products: [],
            messages: [],
            errors: [],
        };
    },

    mounted() {
        this.loadProdcuts();
    },

    methods: {
        loadProdcuts() {
            
            axios.get("http://localhost:3000/products")
            .then(({ data }) => {
                console.log(data);
                this.products = data;
            })
            .catch(err => this.errors.push("Une erreur s'est produite:" + err));
        },
    },
};
</script>