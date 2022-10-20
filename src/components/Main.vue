<template>
<div>
  <div>
    <vue-good-table
      :columns="columns"
      :rows="rows"
      :search-options="{
    enabled: true,
    
  }"
  :pagination-options="{
    enabled: true,
    mode: 'records',
    perPage: 5,
    position: 'top',
    perPageDropdown: [5,10],
    dropdownAllowAll: false,
    setCurrentPage: 2,
    nextLabel: 'next',
    prevLabel: 'prev',
    rowsPerPageLabel: 'Rows per page',
    ofLabel: 'of',
    pageLabel: 'page', 
    allLabel: 'All',
  }"
  />
  </div>
</div>
</template>

<script lang="ts">
import Vue from 'vue';
import axios from "axios";
import * as VueGoodTable from 'vue-good-table';

Vue.use(VueGoodTable.default);
export default Vue.extend({
  name: 'MainComponent',
  data(){
      return {
        body:'',
        id:'',
        title:'',
        searchTerm:'',
        data:{},
        columns: [
        {
          label: 'Id',
          field: 'id',
        },
        {
          label: 'Title',
          field: 'title',
          type: 'string',
        },
        {
          label: 'Body',
          field: 'body',
          type: 'string',
        }
        
      ],
      rows: [
        { id:'', title:"",body: '' },
        { id:'', title:"",body: ' ' },
        { id:'', title:"",body: '' }  
      ],
      }
    },
    mounted() {
      axios.get('https://jsonplaceholder.typicode.com/posts')
      .then((response) => {
           console.log('----->',JSON.parse(JSON.stringify(response.data)));   
           this.rows = response.data;
      }).catch((error) =>{
         console.log(error);  
      });     
    },
    components: {
      'vue-good-table': require('vue-good-table').VueGoodTable
    }
});
</script>


<style scoped>

</style>
