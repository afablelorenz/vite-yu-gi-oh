<script>
import YugiCards from './YugiCards.vue'
import axios from 'axios';
export default{
    components:{
        YugiCards,
    },
    data(){
        return{
            yugiCardsList: [],
            yugiCardsListImg:[],
        }
    },
    methods:{
        getYugiCards(){
            axios.get('https://db.ygoprodeck.com/api/v7/cardinfo.php?num=20&offset=0')
            .then((response) => {
                console.log(response.data.data);
                this.yugiCardsList = response.data.data;
            })
            .catch(function (error) {
                // handle error
                console.log(error);
            })
            .finally(function () {
                // always executed
            });
        },
        
    },

    created(){
        this.getYugiCards();
    }
};
</script>

<template>
    <main>
        <div class="container">
            <div class="cardContainer">
                <YugiCards :yugiCardsList = "yugiCardsList"/>
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
    height: 89.1vh;
    background-color: white;
    width: 80%;
}
</style>