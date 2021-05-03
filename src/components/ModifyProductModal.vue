<template>
    <div class="box">
        <form action="">
            <div class="field">
                <label class="label">Nom</label>
                <div class="control">
                    <input class="input" type="text" v-model="product.name" />
                </div>
            </div>

            <div class="field has-addons">
                <label class="label">Prix unité</label>
                <div class="control">
                    <input
                        class="input"
                        type="number"
                        v-model.number="product.price"
                    />
                </div>
                <div class="control">
                    <a class="button is-static"> € </a>
                </div>
            </div>

            <div class="field has-addons">
                <label class="label">Tags</label>
                <div class="control">
                    <input class="input" type="text" />
                </div>
                <div class="control">
                    <a class="button is-primary"> Ajouter </a>
                </div>
                <div class="tag mt-3 mb-1">
                    <span v-for="tag in product.tags" :key="tag.id" class="tag is-primary is-light mr-2">{{ tag.name }} <button class="delete is-small"></button></span>
                </div>
            </div>


        </form>
    </div>
</template>

<script>
export default {
    props: ["dataProduct"],

    data() {
        return {
            product: this.dataProduct,
        };
    },

    computed: {
        basketTotal() {
            return this.basket.products.reduce(
                (accumulator, product) =>
                    accumulator + product.basket_quantity * product.price,
                0
            );
        },
    },

    methods: {
        closeModal() {
            this.$emit("closeModal");
        },
    },
};
</script>