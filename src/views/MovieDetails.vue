<template>
<div id="main_Details">
    
    <section id="details_block">
        <div class="movie_poster">
            <img :src="`http://image.tmdb.org/t/p/w500/${movieDetails.poster_path}`">
        </div>

        <div class="movie_details_block">
            <h2 class="title green_text">{{movieDetails.title}}</h2>
            <h3 class="tagline" v-if="movieDetails.tagline">"{{movieDetails.tagline}}"</h3>
            <br>
            <p class="storyline"><strong class="green_text">Story Line:</strong>  {{movieDetails.overview}}</p>
            <br>
            <br>

            <div class="credits_block">
                <div class="cast_block">
                    <span class="cast_head">Cast</span>
                    <div class="cast_container">
                        <div class="cast_list">
                            <table>
                                <thead>
                                    <tr>
                                        <th>Cast</th>
                                        <th>Character Played</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr class="cast_details" v-bind:key="cast.id" v-for="cast in movieDetails.credits.cast">
                                        <td>{{cast.name}}</td>
                                        <td>{{cast.character}}</td>
                                    </tr>
                                </tbody>    
                            </table>
                        </div>
                    </div>
                </div>

                <div class="crew_block">
                    <span class="crew_head">Crew</span>
                    <div class="crew_container">
                        <div class="crew_list">
                            <table>
                                <thead>
                                    <tr>
                                        <th>Crew</th>
                                        <th>Job</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr class="crew_details" v-bind:key="crew.id" v-for="crew in movieDetails.credits.crew">
                                        <td>{{crew.name}}</td>
                                        <td>{{crew.job}}</td>
                                    </tr>
                                </tbody>    
                            </table>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>

</div>
</template>

<script>
import axios from "axios";
export default {
    data() {
        return {
            movieDetails: []
        }
    },
    created() {
        var vm= this;
        axios.get(`https://api.themoviedb.org/3/movie/${this.$route.params.id}?api_key=642cd3357bcf98c5781401017fdac7d1&append_to_response=videos,images,credits`)
        .then((response) => {
            console.log(response);
            vm.movieDetails = response.data;
        })
    }
};
</script>

<style lang="scss" scoped>

#details_block {

    .movie_poster {
        width: 100%; 

        img {
            width: 50%;
            max-height: 700px;
        }
    }
    

    .green_text {
        color: #42b983;
    }

    .tagline {
        font-style: italic;
        font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
        font-weight: 300;
    }

    .storyline {
        line-height: 1.8;
        letter-spacing: .8px;
        padding: 10px;
    }

    .cast_head, .crew_head {
        background-color: #42b983;
        color: #222;
        display: block;
        padding: 15px 0;
        margin: 0 20px;
        border-radius: 50px;
        font-weight: bold;
    }

    .cast_container, .crew_container {
        background-color: #222;
        margin: 15px;
        padding: 20px;
        height: 250px;
        overflow: auto;
        border-radius: 10px;

        table {
            border-collapse: collapse;
            width: 100%;

            thead {
                th {
                    color: #42b983;
                    font-size: 1.1em;
                    padding-top: 0;
                }
            }
        
            th, td {
                text-align: center;
                padding: 12px;
                width: 50%;
            }

            tbody {

                tr:nth-child(even) {background-color: #777; color: #111;}

                tr:first-child {border-top-left-radius: 50px;}

                tr:nth-child(odd) {background-color: #333;}
            }
        }
    }
}

@media only screen and (min-width: 550px) {
    .credits_block {
        display: flex;
        justify-content: space-evenly;
    }
}

@media only screen and (min-width: 1024px) {
    #details_block {
        display: flex;

        .movie_poster {
            width: 100%;
        }

        .movie_poster img {
            width: 75%;
            min-width: 400px;
        }

        .credits_block {
            .cast_block, .crew_block {
                width: 50%;
            }
        }
    }
}

</style>