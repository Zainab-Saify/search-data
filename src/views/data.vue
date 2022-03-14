<template>

<div class="mt-12 ">
    <v-layout justify-center align-center> <h2>Employee Data Table</h2></v-layout>
    <v-btn class="ml-5 mb-5" @click="addNewFilter"  >Filter table</v-btn>
    <v-layout row>
        <div v-for="filter in addedFilters" :key="(filter.field, filter.value, filter.filter)">
        <cusfilter @addFilter="addFilter" @removeFilter="removeFilter"  :prop_field="filter.field" :prop_value="filter.value" :prop_filter="filter.filter" :prop_added="filter.field == null? false: true"></cusfilter>
        </div>
    </v-layout>
    <v-data-table
    :headers="headers"
    :items="filteredData"
    hide-default-footer
    :items-per-page="10000"
    class="elevation-1 mt-12 pt-12">

    </v-data-table>

</div>
  
</template>

<script>
import json from '../../json/borrowers.json'
import cusfilter from '../components/filter.vue'
export default {

    components: {
        cusfilter
    },

    data: () => ({
        data: json,
      
        addedFilters: [],
        filteredData: json,
        headers: [
          {
            text: 'First Name',
            align: 'start',
            sortable: false,
            value: 'firstName',
          },
          { text: 'Last Name', value: 'lastName' },
          { text: 'DOB', value: 'dateOfBirth' },
          { text: 'Credict Score', value: 'creditScore' },
          { text: 'Marital Status', value: 'maritalStatus' },
          { text: 'Income', value: 'w2Income' },
          { text: 'Home ph.', value: 'homePhone' },
          { text: 'Email', value: 'emailAddress' },
          { text: 'cell ph.', value: 'cellPhone' },
          { text: 'Current Address', value: 'currentAddress' },
          { text: 'Employer', value: 'employer' },
          { text: 'Title', value: 'title' },
          { text: 'Start Date', value: 'startDate' },
          { text: 'subjectPropertyAddress', value: 'subjectPropertyAddress' },




        

        ],

    }),

    watch: {


    },

    methods: {

        addNewFilter: function(){
            this.addedFilters.push({ field:null, filter:null, value:null})
            

 
        },

        addFilter: function(filter){
             this.removeFilter(null, null, null)
            this.addedFilters.push(filter)
            this.filterData()

        },

         removeFilter: function(field, filter, value){
             this.filteredData = this.data
            
            this.addedFilters.splice(this.addedFilters.findIndex(a => a.field === field && a.filter === filter && a.value === value) , 1)
            this.filterData()


        },

         filterData: function(){
            for(var i = 0; i < this.addedFilters.length; i++){
                var filter = this.addedFilters[i]
               
                var result = []
                if(filter.field.type == 'string'){
                    if(filter.filter == 'contains'){
                    this.filteredData.map( data => { if(`${data[filter.field.value]}`.includes(filter.value)) {result.push(data)}   })
                   
                    this.filteredData = result
                    }
                    else{
                    this.filteredData.map( data => { if(`${data[filter.field.value]}` === filter.value) {result.push(data)}   })
                  
                    this.filteredData = result
                    
                    }
                }
                else{
                    if(filter.field.type == 'number'){
                        if(filter.filter == 'less than'){
                        this.filteredData.map( data => { if(`${data[filter.field.value]}` < parseInt(filter.value)) {result.push(data); }   })
                     
                        this.filteredData = result
                    }
                    if(filter.filter == 'more than'){
                        this.filteredData.map( data => { if(`${data[filter.field.value]}` > parseInt(filter.value)) {result.push(data); }   })
                    
                        this.filteredData = result
                    }
                    if(filter.filter == 'equals'){
                        this.filteredData.map( data => { if(`${data[filter.field.value]}` == parseInt(filter.value)) {result.push(data);}   })
                    
                        this.filteredData = result
                    }

                    }
                    else{
                        if(filter.field.type == 'date'){
                            var parts = filter.value.split('/');
                            var value = new Date(parts[2], parts[0] - 1, parts[1]);
                            var compareDate;

                        

                            if(filter.filter == 'less than'){
                            this.filteredData.map( data => {
                            parts =`${data[filter.field.value]}`.split('/');
                            compareDate = new Date(parts[2], parts[0] - 1, parts[1]);
                          
                            if(compareDate < value){result.push(data)}}
                            )}

                            

                            if(filter.filter == 'more than'){
                            this.filteredData.map( data => {
                            parts =`${data[filter.field.value]}`.split('/');
                            compareDate = new Date(parts[2], parts[0] - 1, parts[1]);
                            if(compareDate > value){result.push(data)}})}

                            if(filter.filter == 'equals'){
                            this.filteredData.map( data => {
                            parts =`${data[filter.field.value]}`.split('/');
                            compareDate = new Date(parts[2], parts[0] - 1, parts[1]);
                            if(compareDate === value){result.push(data)}})}

                            this.filteredData = result


                            }

                    }
                            

                        }

                    }
                }
            
        },

    computed: {
       
    },



}
</script>

<style>

</style>