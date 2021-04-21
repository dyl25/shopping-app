<template>
    <div class="modal" :class="{'is-active': visible}">
        <div class="modal-background"></div>
        <div class="modal-content">
            <slot></slot>
        </div>
        <button @click="close" class="modal-close is-large" aria-label="close"></button>
    </div>
</template>

<script>

export default {
    props: ['dataVisible'],

    data() {
        return {
            visible: this.dataVisible
        };
    },

    watch: {
        dataVisible: function(val) {
            this.visible = val
        }
    },

    mounted() {
    },

    methods: {
        close() {
            this.$emit('closeModal')
            this.visible = false
        }
    },
};
</script>