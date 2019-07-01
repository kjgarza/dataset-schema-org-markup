<template>
  <div class="schemaOrg">
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'DatasetSchemaOrgMarkup',
  props: {
    doi: {
      type: String,
      required: true,
      validator: function (value) {
        return value.match(/^[A-Za-z0-9][-._;()/:A-Za-z0-9]+$/) !== -1
      }
    }
  },
  data: function(){
    return{
      domain: "https://data.datacite.org",
      markup: null,
      uri: 'https://data.datacite.org/application/vnd.schemaorg.ld+json/https://doi.org/' 
    }
  },
  computed:{
    url: function(){
      return this.uri + this.doi
    }
  },
  mounted () {
    axios
      .get(this.url,
        {
        params: {
          email: "dataset-schema-org-markup-component"
        }
      } )
      .then(response => {
        this.markup = response.data
        let tag = document.createElement('script')    
        tag.setAttribute('type',"application/ld+json")
        tag.text = JSON.stringify(this.markup)
        document.head.appendChild(tag)
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
  }
}
</script>
<style scoped>
</style>
