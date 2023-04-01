<template>
    <div
      class="main-card-wrapper"
    >
        <div class="main-card">
           <div class="x-ray">
            <h3 class="card-subsection-title"  style="border-bottom:1px solid #E0E0E0">X-Ray</h3>
           </div>
           <div class="x-ray" style="border-bottom:1px solid #E0E0E0">
            <h3 class="card-subsection-title">Ultrasound Scan</h3>
           </div>
           <div>
           </div>
        </div>
    </div> 
</template>
  
  <script>
  import gql from 'graphql-tag'
  export default {
    name: 'MainCard',
    data() {
      return {
        token:''
      }
    },
     beforeMount() {
      // await this.getToken()
    },
    methods: {
      // Get bearer token
      async getToken() {
       try {
        const { data: { login }} = await this.$apollo.mutate({
          mutation: gql`mutation ($email: String! $password: String!) {
            login(email: $email password:$password) 
          }`,
          variables:{
            email: 'tester@kompletecare.com',
            password: 'password'
          }
        })
        await this.$apolloHelpers.onLogin(login)
       } catch (error) {
        console.log("error", error)
       }
      }
    }
  }
  </script>