<script setup>
    import { useMovieStore } from "../stores/MovieStore" ;
    import { useSearchStore } from "../stores/SearchStore";


    const movieStore = useMovieStore();
    const searchStore = useSearchStore();
    const props = defineProps({
        movie: {
            type: Object,
            required: true,
            default: () => {},
        },
        isSearch: {
            type: Boolean,
            required: false,
            default: false,
        },
    });
    
</script>

<template>
    <div class="movie">
        <img
            :src="`https://image.tmdb.org/t/p/w300_and_h450_bestv2${movie.poster_path}`"
            :alt="movie.original_title"
            class="movie__img"  
        />
        <div>
            <div class="movie__name">
                {{ movie.original_title }} ({{ movie.release_date }})
            </div>
            <span class="movie__overview">
                {{ movie.overview }}
            </span>
            <div class="movie__buttons" v-if="!isSearch">
                <button 
                    class="btn movie__buttons__watched"
                    @click="movieStore.toggleWatched(movie.id)">
                    <span v-if="!movie.isWatched">Watched</span>
                    <span v-else>Unwatched</span>
                </button>
                <button 
                    class="btn movie__buttons__delete"
                    @click="movieStore.deleteMovie(movie.id)">
                    Delete
                </button>
            </div>
            <div class="movie-buttons" v-else>
                <button 
                class="btn btn__green"
                @click="searchStore.addToUserMovies(movie)">
                Add
            </button>
        </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.movie {
    display: grid;
    grid-template-columns: 200px 1fr;
    column-gap: 30px;
    margin-bottom: 20px;
    border: 2px solid #efefef;
    padding: 10px;
    border-radius: 10px;
		// .movie__img
		&__img {
            width: 200px;
            height: 200px;
            object-fit: cover;
            border-radius: 50%;
        }
		// .movie__name
		&__name {
            display: flex;
            align-items: center;
            font-size: 20px;
            margin-bottom: 20px;
        }
		// .movie__overview
		&__overview {
            display: block;
            margin-bottom: 20px;
        }
		// .movie__buttons
		&__buttons {
            display: flex;
            align-items: center;
            justify-content: center;
        }
}
.btn {
    border-radius: 10px;
    margin: 0 10px 0 10px;
    color: #fff;
    width: 80px;
    height: 30px;
    &:hover{
        cursor: pointer;
    }
    &:active{
        position: relative;
        left: 2px;
        top: 2px;
    }
    
}
.movie__buttons__watched {
    background: #1eb4c3;
    &:hover{
        background-color: #317177;
    }
    &:active{
        background: #1eb4c3;
    }
    // &__icon {
    //     width: 15px;
    //     margin-left: 10px;
    // }
}
.movie__buttons__delete {
    background: #ff2a2a;
    &:hover{
        background-color:#af2c2c;
    }
    &:active{
        background: #ff2a2a;
    }
}
.btn__green{
    background-color: green;
    &:hover{
        background-color:rgb(69, 221, 69);
        color: black;
    }
    &:active{
        background: green;
        color: #fff;
    }
}




// .movie-accept {
//     margin-right: 10px;
// }



// .movie-buttons-watched__icon {
//     width: 15px;
//     margin-left: 10px;
// }


</style>