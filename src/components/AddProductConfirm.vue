<template>
    <div class="box">
        <article class="px-4 columns mt-3">
            <div class="column">
                <img :src="'./img/'+product.image" alt="">
            </div>
            <div class="column">
                <div>
                    <h3 class="is-size-4 is-inline-block mr-3">
                        {{ product.name }}
                    </h3>
                    <span
                        class="tag is-info is-light is-inline-block is-medium"
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
        <p>Ajouter ce produit au panier?</p>
    </div>
</template>

<script>
export default {
    props: ["dataVisible", "product"],

    data() {
        return {
            visible: this.dataVisible,
        };
    },

    watch: {
        dataVisible: function (val) {
            this.visible = val;
        },
    },

    mounted() {},

    methods: {
        close() {
            this.$emit("closeModal");
            this.visible = false;
        },
    },
};
</script>