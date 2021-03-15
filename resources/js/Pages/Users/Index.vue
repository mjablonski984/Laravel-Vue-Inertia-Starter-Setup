<template>
  <layout>
    <div class="container">
        <!-- TO DISPLAY SHARE DATA :register data in AppServiceProvider in register method 
          example:  Inertia::share('successMessage', function () { return ...} });-->
      <div v-if="successMessage" class="alert alert-success mt-4">
        {{ successMessage }}
      </div>

      <div class="my-5">
        <inertia-link href="/users/create" class="btn btn-primary">Create User</inertia-link>
      </div>
      <table class="table table-striped">
        <thead>
          <tr>
            <th scope="col">Name</th>
            <th scope="col">Email</th>
            <th scope="col">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id">
            <td>{{ user.name }}</td>
            <td>{{ user.email }}</td>
            <td>
              <inertia-link :href="`/users/${user.id}/edit`">Edit</inertia-link>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </layout>
</template>

<script>
// extend layput component
import Layout from '../Layout/Layout'

export default {
    name: 'Index',
     props: ['users', 'successMessage'],

    components: {
        Layout
    },
}
</script>
