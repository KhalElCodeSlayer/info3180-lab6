<template>
    <div>
        <form @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
            <div class="input-group mx-sm-3 mb-2">
                <label class="visually-hidden" for="search">Search</label>
                <input type="search" name="search" v-model="searchTerm"
                id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter
                search term here" />
                <button class="btn btn-primary mb-2">Search</button>
            </div>
            <p>You are searching for {{ searchTerm }}</p>
        </form>
        <div class = "newsGrid news__list">
            <div class="news__item card" v-for="article in articles"> 
                <img class="card-img-top" :src= article.urlToImage alt="Card image cap">
                <h2 class="card-title"> {{ article.title }} </h2>
                <p class="card-text">{{ article.description }}</p>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                articles: [],
                searchTerm: ''
            };
        },
        created() {
            let self = this;

            fetch('https://newsapi.org/v2/top-headlines?country=us',
            {
                headers: {
                    //code shown in lab document did not work had to copy and paste actual api key then copy and paste the code and it somehow worked..not sure why
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
        methods: {
            searchNews() {
                let self = this;

                fetch('https://newsapi.org/v2/everything?q='+ self.searchTerm + '&language=en',
                {
                    headers: {
                        'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
                    }
                })
                .then(function(response) {
                    return response.json();
                })
                .then(function(data) {
                    console.log(data);
                    self.articles = data.articles;
                });
            }
        }
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


/* img{

} */
</style>