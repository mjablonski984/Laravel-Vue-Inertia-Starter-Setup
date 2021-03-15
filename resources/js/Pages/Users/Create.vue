<template>
  <layout>
    <div class="container">
      <div class="col-md-6">
         <!-- TO DISPLAY SHARE DATA :register data in AppServiceProvider in register method 
          as  Inertia::share('successMessage', function () { return ...} });-->
        <div v-if="Object.keys(errors).length > 0" class="alert alert-danger mt-4">
          {{ errors[Object.keys(errors)[0]] }}
        </div>

        <form action="/users" method="POST" class="my-5" @submit.prevent="createUser">
          <div class="form-group">
            <label for="name">Name</label>
            <input type="text" class="form-control" id="name" placeholder="Name" v-model="form.name">
          </div>
          <div class="form-group">
            <label for="email">Email</label>
            <input type="email" class="form-control" id="email" placeholder="Email" v-model="form.email">
          </div>
          <div class="form-group">
            <label for="password">Password</label>
            <input type="password" class="form-control" id="password" placeholder="Password" v-model="form.password">
          </div>
          <button type="submit" class="btn btn-primary">Create User</button>
        </form>
      </div>
    </div>
  </layout>
</template>

<script>
// extend layput component
import Layout from '../Layout/Layout'

export default {
    name: 'Create',
    props: ['errors'],
    components: {
        Layout,
    },
    data() {
        return {
        form: {
            name: '',
            email: '',
            password: '',
        }
        }
    },
    methods: {
        createUser() {

        // Post to inertia controller with this.$inertia
        // (Don't have to use axios etc when using this.$inertia)
        
        this.$inertia.post('/users', this.form)
            .then(() => {
            // code
            }).catch( err => console.log(err))
        }
  }
}
</script>
