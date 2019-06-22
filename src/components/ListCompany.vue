<template>

    <div>
        <ul>
            <li v-for="com in company.data.data" :key="com.id">{{com.name}}
                <ul>
                    <li>year = {{com.yearFounded}}</li>
                    <li>Revenue = {{com.revenue}}</li>

                    </ul>
                    <br/>
            </li>
        </ul>
    <br/>
    
    <h1>Edit entries</h1>
    <input v-model="id" placeholder="ID"/> <br/>
    <input v-model="name" placeholder="Name"/> <br/>
    <input v-model="yearFounded" placeholder="Year"/><br/> 
    <input v-model="revenue" placeholder="revenue"/> <br/>
    <button @click="getCompany">Get record</button>
    <button @click="updateCompany">Update record</button>
    <button @click="postCompany">Add record</button>
    <button @click="deleteCompany">Delete record</button>

    </div>
</template>

<script>
import axios from 'axios'

    const api = axios.create({
      baseURL: 'http://localhost:4000',
      headers: { 'Content-Type': 'application/json' }
    })
export default {
  components: {
  },
  props: {

  },
  methods:{
      async getCompany(){
          this.company = await api.get(`/company/${this.id}`)
      },
      async updateCompany(){
          const body = {
            "name": this.name,
            "yearFounded" : this.yearFounded,
            "revenue" : this.revenue
          }
          await api.put(`/company/${this.id}`, body)
      },
      async postCompany(){
          const body = {
            "name": this.name,
            "yearFounded" : this.yearFounded,
            "revenue" : this.revenue
          }
          await api.post(`/company`, body)
      },
      async deleteCompany(){
          await api.delete(`/company/${this.id}`)
      }
  },
  data () {
    return {
        company:[],
        id:null,
        name:null,
        yearFounded:null,
        revenue:null
    }
  },
  async created () {
    this.company = await api.get('/company')
  }
}
</script>

<style lang="scss">

</style>
