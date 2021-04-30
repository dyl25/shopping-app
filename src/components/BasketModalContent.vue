<template>
    <div class="box">
        <h2 class="is-size-3 px-4">
            Mon panier -
            <span class="has-text-info"> {{ basketTotal }} €</span>
        </h2>

        <p v-if="!basket.products.length" class="has-text-centered">
            Votre panier est vide
        </p>
        <article
            v-for="product in basket.products"
            :key="product.id"
            class="px-4 level mt-3"
        >
            <div class="level-item has-text-centered">
                <figure class="image is-128x128">
                    <img :src="'./img/' + product.image" alt="" />
                </figure>
            </div>
            <div class="level-item has-text-centered">
                <div>
                    <h3 class="is-inline-block mr-3">
                        {{ product.name }} (<span class="has-text-link">{{ product.price }}€</span>/unité)
                    </h3>
                </div>
            </div>

            <div class="level-item has-text-centered">
                <div class="select is-primary">
                    <select
                        @change="updateBasketQuantity(product.id)"
                        v-model="product.basket_quantity"
                    >
                        <option
                            v-for="i in 10"
                            :key="i"
                            v-text="i"
                            :selected="i === product.basket_quantity"
                        ></option>
                    </select>
                </div>
            </div>

            <div class="level-item has-text-centered">
                <span class="tag is-info is-light is-inline-block is-medium"
                    >{{ product.price * product.basket_quantity }} €</span
                >
            </div>

            <div class="level-item has-text-centered">
                <i
                    @click="removeFromBasket(product.id)"
                    class="has-text-danger is-clickable fas fa-trash mr-3"
                ></i>
            </div>
        </article>
    </div>
</template>

<script>
import axios from "axios";

export default {
    props: ["dataVisible", "dataBasket"],

    data() {
        return {
            basket: this.dataBasket,
        };
    },

    computed: {
        basketTotal() {

            return this.basket.products.reduce(
                (accumulator, product) =>
                    accumulator + product.basket_quantity * product.price,
                0
            )
        },
    },

    /* watch: {
        dataVisible: function (val) {
            this.visible = val;
        },
    },*/

    mounted() {},

    methods: {
        updateBasketTotal() {
            this.basket.total = this.basketTotal;
        },

        updateBasketQuantity() {

            this.updateBasketTotal();

            axios
                .put(
                    "http://localhost:3000/baskets/" + this.basket.id,
                    this.basket
                )
                .catch((err) => console.log(err));
        },

        removeFromBasket(productId) {
            let productToRemove = this.basket.products.find(
                (product) => product.id == productId
            );

            this.basket.total -=
                productToRemove.basket_quantity * productToRemove.price;

            this.basket.products = this.basket.products.filter(
                (product) => product.id !== productId
            );
            axios
                .put(
                    "http://localhost:3000/baskets/" + this.basket.id,
                    this.basket
                )
                .catch((err) => console.log(err));
        },
    },
};
</script>