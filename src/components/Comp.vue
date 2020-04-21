<template>

  <div>

    <p>Hello World</p>
      {{directory}}

  </div>

</template>

<script>
import axios from 'axios';
  export default{
    name: 'CompanyData',
    data(){
      return {
          directory: []
      }
  },

  async mounted () {
      try {
        var result = await axios({
            method: "POST",
                url: "http://localhost:8000/graphql/",
                    data: {
                query: `
    				{
					  allTitles {
					    edges {
					      node {
					        id
					        titleName          
					      }
					    }
					  }
					}
    				`
                }
            });
            this.directory = result.data.data.allTitles;
        } catch (error) {
            console.error(error)
        }
    }
  }

      

</script>

<style scoped>
p {
    margin: 40px;
    text-align: center;
    color: green;
    margin: auto;
}
</style>