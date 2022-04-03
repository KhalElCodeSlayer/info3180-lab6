<template>
    <div class = "newsGrid news__list">
        <div v-for="article in articles" class="news__item card"> 
            <img class="card-img-top" :src= article.urlToImage alt="Card image cap">
            <h2 class="card-title"> {{ article.title }} </h2>
            <p class="card-text">{{ article.description }}</p>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                articles: []
            };
        },
        created() {
            let self = this;

            fetch('https://newsapi.org/v2/top-headlines?country=us',
        {
            headers: {
                //code shown in lab document did not work had to copy and paste actual api key
                'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}` 
            }
        })
            .then(function(response) {
                return response.json();
            })
            .then(function(data) {
                console.log(data);
                self.articles=data.articles;
            });
        },
    }
</script>

<style scoped>
.newsGrid {
    display:grid;
    grid-gap:15px;
    grid-template-columns: auto auto auto; 
}

.card{
    width:350px;
    margin:10px;
}


img{

}
</style>