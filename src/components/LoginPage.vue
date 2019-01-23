<template>
  <div class="container">
    <form>
      <div class="row">
        <div class="col-xs-12 col-sm-offset-2 col-md-offset-3">
          <h1>SignUp</h1>
          <hr>
          <div class="form-group">
            <label for="mobile_number">Mobile Number</label>
            <vue-tel-input
              v-model="data.mobile_number"
              @onInput="onInput"
              :preferredCountries="['us', 'gb', 'ua']"
            ></vue-tel-input>
          </div>
          <div class="form-group">
            <label for="password">Password</label>
            <input type="password" id="password" v-model="data.password" class="form-control">
          </div>
          <div class="form-group">
            <label for="password">Password Confirmation</label>
            <input type="password" id="password_confirmation" v-model="data.password_confirm" class="form-control">
          </div>
          <div class="form-group">
            <label for="email">Email</label>
            <input type="email" id="email" v-model="data.email" class="form-control">
          </div>
          <div class="form-group">
            <label for="full_name">Full Name</label>
            <input type="full_name" id="full_name" v-model="data.name" class="form-control">
          </div>
          <div class="row">
            <div class="col-xs-12 col-sm-offset-2 col-md-6 col-md-offset-3">
              <button class="btn btn-primary" @click.prevent="submitted">Submit</button>
            </div>
          </div>
          <hr>
          <button class="btn btn-primary" @click="fetchData">Get Data</button>
          <ul class="list-group">
            <li class="list-group-item" v-for="u in users" :key="u.id">{{ u.username}}</li>
          </ul>
        </div>
      </div>
    </form>
  </div>
</template>
<script>
import 'vue-tel-input/dist/vue-tel-input.css'

export default {
  data () {
    return {
      data: {
        mobile_number: '',
        password: '',
        password_confirm: '',
        email: '',
        name: ''
      },
      users: [],
      isSubmitted: false
    }
  },
  methods: {
    submitted () {
      this.isSubmitted = true
      this.$http.post('https://tradebook-d7710.firebaseio.com/users/data.json', this.data)
        .then(response => {
          console.log(response)
        }, error => {
          console.log(error)
        })
    },
    fetchData () {
      this.$http.get('https://api.tradebuk.com/api/v1/auth/data.json')
        .then(response => {
          return response.json()
        })
        .then(data => console.log(data))
    },
    onInput ({number, isValid, country}) {
      console.log(number, isValid, country)
    }
  }
}
</script>
<style scoped>

</style>
