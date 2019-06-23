<template>

    <div>
        <ul>
            <li v-for="com in company.data.data" :key="com.id">{{com.name}}
                <ul>
                    <li>year = {{com.yearFounded}}</li>
                    <li>Revenue = {{com.revenue}}</li>
                    <li> UUID = {{com._id}}</li>

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
    <button @click="postCompany">Create company</button>
    <button @click="getCompany">Read company</button>
    <button @click="updateCompany">Update company</button>
    <button @click="deleteCompany">Delete company</button>

    </div>
</template>

<script>
import axios from 'axios'

    const api = axios.create({
      baseURL: 'https://gentle-fjord-95536.herokuapp.com',
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
          this.getCompanies()
      },
      async postCompany(){
          const body = {
            "name": this.name,
            "yearFounded" : this.yearFounded,
            "revenue" : this.revenue
          }
          await api.post(`/company`, body)
          this.getCompanies()
      },
      async deleteCompany(){
          await api.delete(`/company/${this.id}`)
          this.getCompanies()
      },
      async getCompanies(){
        this.company = await api.get('/companies')
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
    this.getCompanies()
  }
}
</script>

<style lang="scss">

</style>
