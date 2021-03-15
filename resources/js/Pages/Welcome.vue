<template>
  <layout>
    <div>
      <p>Welcome page {{ foo }}</p>
        <!-- Go to /users without full reload of a page -->
        <inertia-link href="/users">Users</inertia-link>
    </div>
  </layout>  
</template>

<script>
// Extend layput component
import Layout from './Layout/Layout'

export default {
    name: 'Welcome',
    props: ['foo'],

    components: {
        Layout
    },
}
</script>
