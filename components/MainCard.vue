<template>
    <div
      class="main-card-wrapper"
    >
        <div class="main-card" v-if="x_rays.length">
           <form action="" @submit.prevent="handleSubmit">
            <div class="x-ray" style="border-bottom: 1px solid #E0E0E0">
              <h3 class="card-subsection-title">X-Ray</h3>
              <div class="row">
                <div class="col-md-12">
                  <b-form-group  v-slot="{ ariaDescribedby }">
                      <b-form-checkbox-group
                        id="checkbox-group-2"
                        v-model="formData.investigations"
                        :aria-describedby="ariaDescribedby"
                        name="flavour-2"
                        class="w-100"
                      >
                      <div class="row">
                        <div v-for ="x_ray in x_rays" :key="x_ray.id"
                        class="col-12 col-sm-6 col-md-4 col-lg-3 mb-4">
                          <b-form-checkbox class="checkbox"  :value="x_ray.id">{{ x_ray.title }}</b-form-checkbox>
                        </div>
                      </div>
                      </b-form-checkbox-group>
                    </b-form-group>
                </div>
              </div>
            </div>
            <div class="x-ray mt-4" style="border-bottom: 1px solid #E0E0E0">
              <h3 class="card-subsection-title">Ultrasound Scan</h3>
              <div class="row">
                <div class="col-md-12">
                  <b-form-group  v-slot="{ ariaDescribedby }">
                      <b-form-checkbox-group
                        id="checkbox-group-2"
                        v-model="formData.investigations"
                        :aria-describedby="ariaDescribedby"
                        name="flavour-2"
                        class="w-100"
                        
                      >
                      <div class="row">
                        <div v-for ="ultrasoundScan in ultrasound_scans" :key="ultrasoundScan.id"
                        class="col-12 col-sm-6 col-md-4 col-lg-3">
                          <b-form-checkbox class="checkbox" :value="ultrasoundScan.id">{{ ultrasoundScan.title }}</b-form-checkbox>
                        </div>
                      </div>
                      </b-form-checkbox-group>
                    </b-form-group>
                </div>
              </div>
            </div>
            <div class="row mt-5">
              <div class="col-md-6 mb-4">
                <h3 class="select-section-title">CT Scan</h3>
                <b-form-select v-model="formData.ctscan" :options="scanOptions" required></b-form-select>
              </div>
              <div class="col-md-6">
                <h3 class="select-section-title">MRI</h3>
                <b-form-select v-model="formData.mri" :options="mriOptions" required></b-form-select>
              </div>
              <div class="col-md-12" v-if="successMessage">
                <b-alert variant="success" show>{{ successMessage }}</b-alert>
              </div>
              <div class="col-md-12">
                <button type="submit" class="save mt-5">
                  <b-spinner v-if="addingMedicalReports" small></b-spinner> Save and Send
                </button>
              </div>
            </div>
            <div>
            </div>
           </form>
        </div>
        <div class="main-card" v-if="loading">
          <div class="text-center">
            <b-spinner variant="success" label="Spinning"></b-spinner>
          </div>
        </div>
    </div> 
</template>
  
  <script>
  import LOGIN_MUTATION  from '../grapql/login.gql'
  import INVESTIGATIONS_QUERY   from '../grapql/getSubscription.gql'
  import ADD_MEDICAL_RECORDS  from '../grapql/addMedicalRecords.gql'
  // import gql from 'graphql-tag'
  export default {
    name: 'MainCard',
    data() {
      return {
        token:'',
        x_rays:[],
        loading: false,
        addingMedicalReports:false,
        scanOptions: [
          { value: null, text: '*Specify' },
          { text: 'Scan needed in the left cerebral hemisphere', value: 'Scan needed in the left cerebral hemisphere' },
          { text: 'Scan needed in the right cerebral hemisphere ', value: 'Scan needed in the right cerebral hemisphere ' },
        ],
        mriOptions: [
          { value: null, text: '*Specify'},
          { text: 'Full body MRI', value: 'Full body MRI' },
          { text: 'Cardiac MR', value: 'Cardiac MR' },
          { text: 'Functional MRI', value: 'Functional MRI'}
        ],
        ultrasound_scans:[],
        successMessage: '',
        formData: {
          investigations: [],
          ctscan: null,
          mri: null,
          developer: 'Developer',
        }
      }
    },
     async beforeMount() {
      await this.getToken()
    },
    methods: {
        handleSubmit() {
        this.successMessage = ''
          this.addingMedicalReports = true
          this.formData.investigations.map( i => parseInt(i))
          this.formData.investigations = this.formData.investigations.map( i => parseInt(i))
          this.$apollo.mutate({
            mutation:ADD_MEDICAL_RECORDS,
            variables:this.formData,
            context: {
              headers: {
                authorization: `Bearer ${localStorage.getItem('token')}`,
              },
            },
          }).then( res => {
            this.$toast.success('Medical Report Successfully Added.').goAway(3000)
            this.addingMedicalReports = false
            this.formData.investigations = []
            this.formData.mri = null
            this.formData.ctscan  = null
          }).catch((e) => {
            this.addingMedicalReports = false
            console.log(e)
          }) 
      },
      async getToken() {
        this.loading = true
        const variables = {
            email: 'tester@kompletecare.com',
            password: 'password'
        }
       try {
        const { data } = await this.$apollo.mutate({
          mutation:LOGIN_MUTATION,
          variables
        })
        console.log(data)
        localStorage.setItem('token', '5203|Zud5myeZDAOWjV01DIASlkDg6CwBuV0Zq2T7LuHp')
         // eslint-disable-next-line camelcase
        const { data: { investigation_types }} = await this.$apollo.query({
          query:INVESTIGATIONS_QUERY,
          context: {
              headers: {
                authorization: `Bearer ${localStorage.getItem('token')}`,
              },
            },
        })
        // I am trying to get the login token but I am getting internal server error
        // I don't have much time so I decided to hardcode it here
        
        // eslint-disable-next-line camelcase
        this.x_rays = investigation_types[0].investigations
        // eslint-disable-next-line camelcase
        this.ultrasound_scans = investigation_types[1].investigations
       } catch (error) {
        console.log("error", error)
       } finally {
        this.loading = false
       }
      }
    }
  }
  </script>