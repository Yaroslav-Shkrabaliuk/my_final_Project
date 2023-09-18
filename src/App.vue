<script setup>
    import Movie from "./components/Movie.vue";   
    import Search from "./components/Search.vue";
    import { useMovieStore } from "./stores/MovieStore";

    const movieStore = useMovieStore();
    const setTab = (id) => {
        movieStore.setActiveTab(id);
    };
</script>

<template>
    <main>
        <header class="header">
            <img src="./assets/images/icons/logo.svg" alt="logo" class="header__logo" />
            <h2>My Favorite Movies</h2>
        </header>
        <div class="tabs">
            <button 
                :class="['btn', { btn_green: movieStore.activeTab === 1 }]"
                @click="setTab(1)">
                Favorite
            </button>
            <button 
                :class="['btn', { btn_green: movieStore.activeTab === 2 }]"
                @click="setTab(2)">
                Search
            </button>
        </div>
        <div class="movies" v-if="movieStore.activeTab === 1">
            <div>
                <h3>
                    Watched Movies (count: {{ movieStore.watchedMovies.length }})
                </h3>
                <Movie 
                    v-for="movie of movieStore.watchedMovies"
                    :key="movie.id"
                    :movie="movie" />
            </div>
            <h3>
                All Movies (count: {{ movieStore.totalCountMovies }})
            </h3>
            <Movie
                v-for="movie of movieStore.movies"
                :key="movie.id"
                :movie="movie" />
        </div>
        <div class="search" v-else>
            <Search/>
        </div>
    </main>
</template>

<style scoped lang="scss">
.header {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
	&__logo {
        max-width: 50px;
        margin-right: 10px;
    }
}
.tabs {
    display: flex;
    justify-content: center;
    margin-bottom: 30px;
}
.movies {
}
.search {
}

.btn {
    border: none;
    width: 100px;
    height: 40px;
    font-size: 14px;
    margin: 0 10px;
    border-radius: 10px;
    cursor: pointer;
    background: #efefef;
    &:hover {
        opacity: 0.7;
    }
    &:active{
        position: relative;
        left: 2px;
        top: 2px;
    }
}

.btn_green {
    background: #37df5c;
}



</style>
