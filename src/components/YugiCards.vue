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
        }
    }
}
</script>


<template>
    <div>
        <div>
            {{ yugiCardsList.length }}
        </div>
        <article v-for="card in yugiCardsList" :key="card.name">
            <img :src="card.card_images[0].image_url">
            <p></p>
            <p></p>
        </article>
    </div>
</template>


<styles scoped>

</styles>