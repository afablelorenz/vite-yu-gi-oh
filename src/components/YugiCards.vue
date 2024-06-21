<script>
    export default{
        components:{
            
        },
        data(){
            return{

            }
        },
        props:{
            yugiCardsList: {
                type: Array,
                required: true,
            },
            selectedArchetype: {
                type:  String,
                default: '',
            },
        },
        computed: {
            filteredCards() {
                if(!this.selectedArchetype){
                    return this.yugiCardsList;
                }
                return this.yugiCardsList.filter(card => card.archetype === this.selectedArchetype);
            },
        },
    }
</script>


<template>
    <div class="cardListWrapper">
        <div class="cardCount container">
            <p>Found {{ filteredCards.length }} cards</p>
        </div>
        <div class="cardListContainer container">
            <article v-for="card in filteredCards" :key="card.name" class="card">
                <img :src="card.card_images[0].image_url">
                <div class="cardDetails">
                    <p>
                        {{card.name}}
                    </p>
                    <p>
                        {{card.archetype}}
                    </p>
                </div>
            </article>
        </div>
    </div>
</template>



<style scoped>

.container{
    display: flex;
    align-self: center;
    width: 70vw;
}

div.cardListWrapper{
    display: flex;
    flex-direction: column;
}

div.cardCount{
    background-color: #212529;
    height: 1vh;
    color: white;
    display: flex;
    align-items: center;
    justify-content: flex-start;
}

div.cardCount p{
    padding: 2rem;
}

div.cardListContainer{
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
}

article.card{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color:#D48F38;
    margin: .5rem;
}

div.cardDetails{
    display: flex;
    flex-direction: column;
    align-items: center;
}

div.cardDetails p{
    padding: 0.3rem;
}

article.card img{
    height: 21rem;
}
</style>