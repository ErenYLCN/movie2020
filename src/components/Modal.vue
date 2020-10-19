<template>
  <div class="modal" id="modal" @click="closeModal()">
      <div class="modal__content" >
          <div class="modal__header">
              <h1 class="modal__title">{{modalTitle}}</h1>
          </div>
          <div class="modal__body">
                
                <div>
                    <img :src="modalPoster" class="poster">
                   <div> <b>Director:  </b>   <span> {{modalDirector}}</span> </div>
                   <div> <b>Genre:     </b>   <span>  {{modalGenre}}</span>   </div>
                   <div> <b>Plot:      </b>   <span> {{modalPlot}}</span>     </div>
                </div>
          </div>
      </div>

  </div>
</template>

<script>
export default {
    name: "Modal",
    props: ["showModal", "modalPoster", "modalTitle", "modalGenre", "modalDirector", "modalPlot"],
    methods: {
        closeModal() {
            var modalState = false;
            this.$emit("close", modalState);
         },
    }
}
</script>

<style scoped>
.modal {
    align-content: center;
    position: fixed;
    display: block;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0,0,0,0.3);
}
.modal__content {
    min-width: 370px;
    width: 600px;
    background: white;
    margin: auto;
}
.modal__header {
    display: block;
    justify-content: space-between;
    align-items: center;
    padding: 7px 10px;
    border-bottom: 1px solid #eee;
}
.modal__title {
    font-weight: normal;
    font-size: 25px;
}
.modal__close { 
    padding: 5px;
    cursor: pointer;
    font-size: 25px;
}  
.modal__body {
    align-content: center;
    padding: 10px;
}
.poster {
  width: 200px;
  margin-right: 15px;
}
.clearfix {
    overflow: auto;
}
</style>