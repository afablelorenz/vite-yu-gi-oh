<script>
export default{
    props: {
        archetypes: {
            type: Array,
            required: true,
        }
    },
    data(){
        return{
            selectedArchetype: '',
        };
    },
    methods: {
        archetypeChange(){
            this.$emit('archetype-selected', this.selectedArchetype);
        },
    },
};
</script>

<template>
    <div>
        <label for="archetypeSelect">
            Archetype:
        </label>
        <select v-model="selectedArchetype" @change="archetypeChange" id="archetypeSelect">
            <option value="">All</option>
            <option v-for="archetype in archetypes" :key="archetype" :value="archetype">
                {{ archetype }}
            </option>
        </select>
    </div>
</template>

<style>

</style>