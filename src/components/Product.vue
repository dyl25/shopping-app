<template>
    <article @click="modifyProduct" class="px-5 py-5 mt-3 hoverable is-clickable">
        <figure>
            <img :src="'./img/'+product.image" alt="">
        </figure>
        <div>
            <h3 class="is-size-4 is-inline-block mr-3">{{ product.name }}</h3>
        </div>
        <div>
            <span class="tag is-primary is-info is-medium">{{ product.price }}€</span>
        </div>
        <div>{{ product.description }}</div>
        <div class="tags mt-3 mb-1">
            <span v-for="tag in product.tags" :key="tag.id" class="tag is-primary is-light">{{ tag.name }}</span>
        </div>
        <div>
            <span class="mr-5" :class="{'has-text-danger': !inStock}">Quantité: {{ product.quantity }}</span>
            <span>{{ product.creation_date }}</span>
        </div>
        <button @click="addProduct" class="button is-fullwidth is-success">+ Ajouter</button>
    </article>
</template>

<script>

export default {
    props: ['product'],
    data() {
        return {
        };
    },

    mounted() {
    },

    computed: {
        inStock() {
            return this.product.quantity > 0
        }
    },

    methods: {
        addProduct() {
            this.$emit('addProduct', this.product.id);
        },

        modifyProduct() {
            this.$emit('modifyProduct', this.product.id)
        }
    },
};
</script>