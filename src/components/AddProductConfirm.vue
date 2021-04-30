<template>
    <div class="box">
        <article class="px-4 columns mt-3">
            <div class="column">
                <img :src="'./img/' + product.image" alt="" />
            </div>
            <div class="column">
                <div>
                    <h3 class="is-size-4 is-inline-block mr-3">
                        {{ product.name }}
                    </h3>
                    <span class="tag is-info is-light is-inline-block is-medium"
                        >{{ product.price }} €</span
                    >
                </div>
                <div>
                    {{ product.description }}
                </div>
                <div class="tags mt-3">
                    <span class="tag is-primary is-light">abdos</span>
                    <span class="tag is-primary is-light">ventre plat</span>
                    <span class="tag is-primary is-light">Three</span>
                </div>
            </div>
        </article>

        <div class="is-centered has-text-centered">
            <p class="has-text-weight-bold is-size-5 mb-3">
                Ajouter ce produit au panier?
            </p>

            <div class="select is-primary mb-3">
                <select v-model="basketQty">
                    <option value="">Quantité</option>
                    <option v-for="i in 10" :key="i" v-text="i"></option>
                </select>
            </div>

            <div>
                <button
                    @click="addProduct"
                    class="button is-success is-medium mr-5"
                >
                    Oui
                </button>
                <button
                    @click="close"
                    class="button is-danger is-outlined is-medium"
                >
                    Non
                </button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";
export default {
    props: ["dataVisible", "dataProduct", "dataBasket"],

    data() {
        return {
            basket: this.dataBasket,
            product: this.dataProduct,
            visible: this.dataVisible,
            basketQty: 1,
        };
    },

    watch: {
        dataVisible: function (val) {
            this.visible = val;
        },
    },

    mounted() {},

    methods: {
        addProduct() {
            if (
                this.basket.products.some(
                    (product) => product.id === this.product.id
                )
            ) {
                let product = this.basket.products.find(
                    (product) => product.id === this.product.id
                );
                product.basket_quantity = this.basketQty;
            } else {
                this.product.basket_quantity = this.basketQty;
                this.basket.products.push(this.product);
            }

            axios
                .put("http://localhost:3000/baskets/1", this.basket)
                .catch((err) => console.log(err));

            this.close();
        },

        close() {
            this.$emit("closeModal");
            this.visible = false;
        },
    },
};
</script>