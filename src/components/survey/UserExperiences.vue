<template>
  <section>
    <base-card>
      <h2>Submitted Experiences</h2>
      <div>
        <base-button @click="load">{{ btntxt }}</base-button>
      </div>
      <ul>
        <survey-result
          v-for="result in results"
          :key="result.id"
          :name="result.name"
          :rating="result.rating"
        :load=" isload"></survey-result>
      </ul>
    </base-card>
  </section>
</template>

<script>
import SurveyResult from './SurveyResult.vue';

export default {
  components: {
    SurveyResult,
  },
  data(){
    return{
      results:[],
      isload:false
     
    }
  },
  computed:{
    btntxt(){
     return this.isload?'Hide Submitted Experiences':'Load Submitted Experiences'
    }
  },
  methods:{
    //get the data from firebase
    async load() {
      try {
        const response = await fetch('https://survey-app-c9cdd-default-rtdb.firebaseio.com/surveys.json');

        if (!response.ok) {
          throw new Error(`HTTP error! Status: ${response.status}`);
        }

        const data = await response.json();
        this.results = data; // assuming the API response is an array of results
        console.log(data);
      } catch (error) {
        console.error('Error:', error);
      }
      this.isload=!this.isload
        
    },
  }
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>