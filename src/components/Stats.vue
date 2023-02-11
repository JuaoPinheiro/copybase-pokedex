<template>
    <article>
        <div class="pokemon-stats">
            <label class="label-stats" v-for="(stat, index) in pokemon.stats" :key="stat.stat.name">
                {{ stat.stat.name }} {{ stat.base_stat }}</label>
        </div>
    </article>
</template>

<script>

export default {
    data() { },
    props: {
        pokemon: Object,
    },
    methods: {
        transform_name(name) {
            if (name.includes("-")) {
                let parts = name.split("-");
                return `${parts[0].charAt(0).toUpperCase()} ${parts[1]
                    .charAt(0)
                    .toUpperCase()}${parts[1].slice(1)}`;
            }
            return name.charAt(0).toUpperCase() + name.slice(1);
        },
    },
};
</script>