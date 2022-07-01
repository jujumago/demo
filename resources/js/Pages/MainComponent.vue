<script>
  import { Head } from '@inertiajs/inertia-vue3'
  import Modal from '@/Jetstream/Modal.vue'
  import Login from './Auth/Login.vue'
  import Register from './Auth/Register.vue'
  export default {
    components: {
      Head,
      Modal,
      Login,
      Register,
    },
    props: {
      
    },
    data: function() {
      return {
        userModal: false,
        userCRUD: 'login',
      }
    },
    methods: {
        userTab(val){
            this.userModal = true
            this.userCRUD = val
        },
    }
  }
</script>
<template>
    <div>
        <Head title="Welcome" />
        <div class="text-right mt-2">
            <template v-if="$page.props.user">
            </template>
            <template v-else>
                <button class="mx-4 p-3 rounded-lg shadow bg-stone-500 text-white" @click="userTab('login')">Login</button>
                <button class="mx-4 p-3 rounded-lg shadow bg-stone-500 text-white" @click="userTab('register')">Register</button>
            </template>
            <modal :show="userModal" @close="userModal = false">
                <template v-if="userCRUD == 'login'">
                    <login></login>
                </template>
                <template v-else>
                    <register></register>
                </template>
            </modal>
        </div>
    </div>
</template>


