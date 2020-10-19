<template>
      <div class="search">
        <input type="text" v-model="searchKey" size="70" placeholder="Search for a movie from 2020..">
        <div>
         <button v-on:click="searchMovie" class="search-btn">Search</button>
        </div>
        <div v-if="movieFound == false">
          <h1>Movie Not Found!</h1>
        </div>
        <div>
          <ul>
            <li v-for="(item, index) in moviesList" :key="index" class="list-item">
              <div v-if="item.Poster !='N/A'" class="poster-div">
                <div title="clickable">
                  <img :src="item.Poster" class="poster">
                  <div class="title"> 
                    <span>{{ item.Title  }}</span>
                    <div>
                      <button class="details-btn" @click="modal(index)" >Details</button>
                    </div>
                  </div>
                </div>
              </div>
            </li>
          </ul>
        </div>
        <div v-if="showModal">
         <Modal :showModal="showModal" :modalPoster="modalPoster" :modalTitle="modalTitle" :modalGenre="modalGenre" :modalDirector="modalDirector" :modalPlot="modalPlot" @close="update"/>
        </div>
      </div>
</template>

<script>
import Modal from "./Modal.vue";

export default {
  name: 'Search',
  components: {
    Modal,
  },
  data() {
    return {
      movieFound: true,
      showModal: false,
      searchKey:'',
      moviesList:[],
      modalPoster: '',
      modalTitle: '',
      modalGenre:'',
      modalDirector:'',
      modalPlot:'',
    };
  },
  methods: {

    searchMovie() {
      if(this.searchKey != '') {
        var url = 'http://www.omdbapi.com/?apikey=933a6f7f&s='+this.searchKey+'&y=2020'
        fetch(url)
          .then(response=> response.json())
          .then(data=> {
        if(data.Search == null) {
          this.movieFound = false;
          this.moviesList = [];
        } else {
          this.movieFound= true;
          this.moviesList = data.Search;
        }
         }
        );
      }
    },
    modal(index) {
      this.modalPoster = this.moviesList[index].Poster;
      var url = 'http://www.omdbapi.com/?apikey=933a6f7f&i='+ this.moviesList[index].imdbID;
      fetch(url)
        .then(response => response.json())
        .then(data => {
          this.modalTitle = data.Title;
          this.modalGenre = data.Genre;
          this.modalDirector = data.Director;
          this.modalPlot = data.Plot;
        });
      console.log(this.modalPlot);
      this.showModal = true;
    },
    update() {
      this.showModal = false;
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display:inline-block;
  margin: 0 10px;
}

.search {
  margin: auto;
  margin-top: 30px;
}
.search-btn {
  margin-top: 15px;
  margin-bottom: 20px;

  appearance: none;
  outline: none;
  border: none;
  background: none;
  cursor: pointer;

  display: inline-block;
  padding: 10px 25px;
  background-image: linear-gradient(to right, #CC235D, #FF5858);
  border-radius: 8px;

  color: #FFF;
  font-size: 18px;
  font-weight: 700;

  box-shadow: 3px 3px rgba(0,0,0,0.4);
  transition: 0.4s ease-out
}
.details-btn {
  margin-top: 5px;

  appearance: none;
  outline: none;
  border: none;
  background: none;
  cursor: pointer;

  display: inline-block;
  padding: 6px 20px;
  background-image: linear-gradient(to right, #CC235D, #FF5858);
  border-radius: 8px;

  color: #FFF;
  font-size: 18px;
  font-weight: 700;

  box-shadow: 3px 3px rgba(0,0,0,0.4);
  transition: 0.4s ease-out;

}
input {
  outline: none;
  border: none;
  background: none;

  border:3px solid #666;
  border-radius: 50px;
  padding: 10px 10px;


}
button:hover {
  box-shadow: 6px 6px rgba(0,0,0,0.6);
}
.poster {
  width: 240px;
  object-fit: contain;
  margin-top: 40px;
}
.poster-div {
  margin-top: 0px;
}
.title {
  word-wrap: break-word;
  width: 240px;
  height: 200px;
  position:absolute;
  margin-top:5px;
}
.list-item {
  height: auto;
  max-height: 400px;
  margin-bottom: 60px;
}
.modal-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom:0;
  z-index: 98;
  background-color: (rgba(255, 0, 0, 0.3));
}
</style>
