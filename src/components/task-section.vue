<template>
      <button v-on:click="addSection()" type="button" class="m-3 btn btn-info text-white"><i class="fas fa-plus"></i> ADD SECTION</button>

    <div  class="d-flex justify-content-start wrap">

      <div v-for="(taskSectionItem,index) in taskSectionList" :key="taskSectionItem" class="col-12 card-width  m-3 bg-light p-2 shadow rounded">
        <input v-model="taskSectionItem.name" id="section-name" type="text" placeholder="Section Name">
        <div class="text_underline"></div>

      <taskItem v-for="(taskItem,index) in taskSectionItem.tasks" :key="taskItem"
      v-bind:val="taskSectionItem.name"
      v-on:removeTask="removeTask(index,taskSectionItem.id)"
      />

        <div class="m-3 px-3  d-flex justify-content-between">
          <button class="plus" v-on:click="addTask(index)">
            <i class="fas fa-plus fa-lg"></i>
          </button>
          <button class="trash" v-on:click="removeSection(index)">
            <i class="fas fa-trash fa-lg"></i>
          </button>
        </div>
      </div>
    </div>
</template>

<script>

import taskItem from './task-item.vue'
export default {
  name: 'taskSection',
  components: {
    taskItem
  },
  data: function(){
    return{
      taskSectionList:[],
      taskSectionId:0,
      taskSectionName:""
    }
  },
  methods:{
    addSection(){
      this.taskSectionId++;
      this.taskSectionList.push(
        {name:this.taskSectionName,
        tasks:[],
        id:this.taskSectionId}
        );
    },
    removeSection(index){
      this.taskSectionList.splice(index,1);
    },
    addTask(index){
      this.taskSectionList[index].tasks.push({sectionId:index});
    },
    removeTask(index,sectionId){
      console.log(this.taskSectionList[sectionId-1].tasks)
      console.log(index)
      this.taskSectionList[sectionId-1].tasks.splice(index,1)
    }
  }

}
</script>

<style>
.plus:hover{
  background-color: #F2F2F2; 
  border-radius: 50%;
  opacity: 0.8;
}
 .trash:hover{
  background-color: #F2F2F2; 
  border-radius: 50%;
  opacity: 0.8;
}
button{
  background-color: transparent;
  border: none;
  cursor: pointer;
  outline: none;
  padding: 0;
  appearance: none;
}
.wrap{
  max-width: 100%;
  overflow-x: auto;
}
.font-sm{
  font-weight: 500;
  font-size: 0.8rem;
}
.card-width{
  width: 250px;
}
#section-name{
  width: 100%;
  border: none;
  outline: none;
  padding-bottom: 8px;
  box-sizing: border-box;
  background-color: transparent;
}

.text_underline{
  position: relative;
  border-top: 1px solid grey ;
}
.text_underline::before,
.text_underline::after{
    position: absolute; 
    bottom: 0px; /*中央配置*/
    width: 0px; /*アニメーションで0pxから50%に*/
    height: 1px; /*高さ*/
    content: '';
    /* border-top: 2px solid grey ; */
    background-color: #15AABF; /*アニメーションの色*/
    transition: all 0.5s;
    -webkit-transition: all 0.5s;
}
/*中央から右へのアニメーション*/
.text_underline::before{
  left: 50%; /*中央配置*/
}

/*中央から左へのアニメーション*/
.text_underline::after{ 
  right: 50%; /*中央配置*/
}

:focus + .text_underline::before,
:focus + .text_underline::after{
  width: 50%;
}


</style>