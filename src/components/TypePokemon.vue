<template>
    <div class="div-types">
        <label class="label-types"> {{ name }}</label>
    </div>
</template>

<script>
export default {
    props: {
        type: String,
    },
    computed: {
        name() {
            return this.type.charAt(0).toUpperCase() + this.type.slice(1);
        },

    },
};
</script>