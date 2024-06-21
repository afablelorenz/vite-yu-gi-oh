<script>
import YugiCards from './YugiCards.vue';
import CardSearch from './CardSearch.vue';
import axios from 'axios';
export default{
    components:{
        YugiCards,
        CardSearch,
    },
    data(){
        return{
            yugiCardsList: [],
            archetypes: [],
            selectedArchetype: '',
        }
    },
    methods:{
        getYugiCards(){
            axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=500&offset=0')
            .then((response) => {
                console.log(response.data.data);
                this.yugiCardsList = response.data.data;
                this.extractArchetypes(this.yugiCardsList);
            })
            .catch(function (error) {
                // handle error
                console.log(error);
            })
            .finally(function () {
                // always executed
            });
        },
        extractArchetypes(cards){
            const archetypesSet = new Set();
            cards.forEach(card =>{
                if (card.archetype){
                    archetypesSet.add(card.archetype);
                }
            });
            this.archetypes = Array.from(archetypesSet);
        },
        updateSelectedArchetype(archetype){
            this.selectedArchetype = archetype;
        }
        
    },
    created(){
        this.getYugiCards();
    }
};
</script>

<template>
    <main>
        <div class="container">
            <CardSearch :archetypes="archetypes" @archetype-selected="updateSelectedArchetype" />
            <div class="cardContainer">
                <YugiCards :yugiCardsList = "yugiCardsList" :selectedArchetype="selectedArchetype" />
            </div>
        </div>
    </main>
</template>

<style>

main{
    background-color: #D48F38;
}

div.container{
    display: flex;
    justify-content: center;
    padding: 1rem;
}

div.cardContainer{
    background-color: white;
    width: 80%;
}
</style>