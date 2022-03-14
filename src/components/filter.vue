<template>
  <div class="ml-10">
      <v-layout justify-space-between class=" mt-2">
          <v-select outlined v-model="field" :items="fieldOptions" label="select field"  return-object dense style="width: 240px; max-width:240px"></v-select>
          <v-select outlined v-model="filter" dense class="ml-2" :items="filterOptions" label="select filter"  style="width: 240px; max-width:240px"></v-select>
          <v-text-field outlined v-model="value" dense class="ml-2"  style="width: 240px; max-width:240px"></v-text-field>
          <v-btn @click="addFilter" class="ml-2"  v-if="!added">Apply</v-btn>
          <v-btn v-else class="ml-2" @click="$emit('removeFilter', field, filter, value)">Remove</v-btn>
      </v-layout>
  </div>
</template>

<script>
export default {

    props:[ 'prop_filter', 'prop_value', 'prop_field', 'prop_added' ],

    created: function(){
        this.field = this.prop_field
        this.filter = this.prop_filter,
        this.value = this.prop_value
        this.added = this.prop_added
    },


    

    data: () => ({

        field: null,
        filter: null,
        value: null,
        
        added: false,
        filterOptions: [],

        fieldOptions: [
          {
            text: 'First Name',
            value: 'firstName',
            type: 'string'
          },
          { text: 'Last Name', value: 'lastName',type: 'string' },
          { text: 'DOB', value: 'dateOfBirth', type: 'date' },
          { text: 'Credict Score', value: 'creditScore', type: 'number' },
          { text: 'Marital Status', value: 'maritalStatus', type: 'string' },
          { text: 'Income', value: 'w2Income', type: 'number'  },
          { text: 'Home ph.', value: 'homePhone', type: 'string' },
          { text: 'Email', value: 'emailAddress', type: 'string' },
          { text: 'cell ph.', value: 'cellPhone',type: 'string' },
          { text: 'Current Address', value: 'currentAddress', type: 'string' },
          { text: 'Employer', value: 'employer', type: 'string' },
          { text: 'Title', value: 'title', type: 'string' },
          { text: 'Start Date', value: 'startDate', type: 'date' },
          { text: 'subjectPropertyAddress', value: 'subjectPropertyAddress', type: 'string' },]


    }),

    methods: {

        addFilter: function(){
            var filter = { field: this.field, filter: this.filter, value: this.value}
            this.$emit('addFilter', filter)
            this.added = true

        },

        

    },

    watch: {
        field: {
            handler(val){
                if(val){
                    if(this.field.type == 'string'){
                        this.filterOptions = ['contains', 'matches excatly']
                    }
                    else{
                        this.filterOptions = ['less than', 'more than', 'equals']
                    }
                }
            }
        }
    }

}
</script>

<style>

</style>