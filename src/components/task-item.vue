<template>
          <div class="d-flex flex-column">
          <div class="m-3 p-3 shadow">
            <input id="section-name" type="text" placeholder="Title">
            <div class="text_underline"></div>

            <div class="my-2 font-sm text-secondary">Section Name:{{val}}</div>
            <div class="my-2 font-sm text-secondary">Memo:</div>

            <div v-if="isFocusMemo">
            <textarea v-model="memo" style="height: 100px;" class="w-100" name="memo" id="" cols="30" rows="10"></textarea>
            </div>
            <div v-else>{{memo}}</div>

            <div class="d-felx justify-content-end">

              <div class="py-3 mr-1 d-flex justify-content-end">
                <button v-on:click="toggleMemo">
                  <i class="fas fa-file-alt  px-1"></i>
                </button>
                <button  v-on:click="toggleCheck">
                  <i class="fas fa-check  px-1"></i>
                </button>
                <button v-on:click="toggleFavorite">
                  <i class="fas fa-star  px-1"></i>
                </button>
                <button  v-on:click="$emit('removeTask')">
                  <i class="fas fa-trash  px-1"></i>
                </button>

              </div>
            </div>
          </div>
        </div>
</template>

<script>


export default {
  name: 'taskItem',
  props:["val"],
  data:function(){
    return{
      memo:"",
      isFocusMemo:false,
      isChecked:false,
      isFavorite:false

    }
  },
  methods:{
    toggleMemo:function(event){
      if(this.isFocusMemo){
        event.currentTarget.classList.remove("memo");
        this.isFocusMemo = false;
      }else{
        event.currentTarget.classList.add("memo");
        this.isFocusMemo  = true;
      }
    },
    toggleCheck:function(event){
       if(this.isChecked){
          event.currentTarget.classList.remove("check"); 
          this.isChecked = false;
       }else{
          event.currentTarget.classList.add("check"); 
          this.isChecked  = true;
       } 
    },
    toggleFavorite:function(event){
      if(this.isChecked){
          event.currentTarget.classList.remove("star"); 
          this.isChecked = false;
      }else{
          event.currentTarget.classList.add("star"); 
          this.isChecked  = true;
      } 
    }
  }
}
</script>

<style scoped>
button:hover{
  background-color: #F2F2F2;
  border-radius: 50%;
}
.star{
  transition: all 0.3s;
  color: #FFEB3B;
}
.trash{
  transition: all 0.3s;
  color: blue;
}
.check{
  transition: all 0.3s;
  color: red;
}
.memo{
  transition: all 0.3s;
  color: yellowgreen;
}
</style>