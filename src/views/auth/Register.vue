<script>
import { ref } from 'vue';
import axios from 'axios';
import { useRouter } from 'vue-router';

export default {
  name: 'Register',
  setup() {
    const name = ref('');
    const email = ref('');
    const password = ref('');
    const password_confirmation = ref('');
    const router = useRouter();
    const validation = ref([]);

    const submit = async () => {
      await axios
        .post('/register', {
          name: name.value,
          email: email.value,
          password: password.value,
          password_confirmation: password_confirmation.value,
        })
        .then(() => {

            alert('registration succesfully');
          router.push({ path: '/login' });
        })
        .catch((error) => {
          validation.value = error.response.data;
        });
    };

    return {
      name,
      email,
      password,
      password_confirmation,
      submit,
      validation,
    };
  },
};
</script>

<template>
  <div class="relative flex flex-col items-center justify-center min-h-screen">
    <span class="px-2 py-2 mb-4 text-red-600 rounded shadow">
      {{ validation.message }}
    </span>

<div class="container">

 <div class="row">
    
    <div class="col-md-6">
    
    
        <form class="space-y-4" @submit.prevent="submit">
        <div>
          <label for="name" class="block text-sm text-gray-800">Name</label>
          <input
            v-model="name"
            name="name"
            type="text"
            class="block w-full px-4 py-2 mt-2 text-purple-700 bg-white border rounded-md focus:border-purple-400 focus:ring-purple-300 focus:outline-none focus:ring focus:ring-opacity-40"
          />
        </div>
        <div>
          <label for="email" class="block text-sm text-gray-800">Email</label>
          <input
            v-model="email"
            name="email"
            type="email"
            class="block w-full px-4 py-2 mt-2 text-purple-700 bg-white border rounded-md focus:border-purple-400 focus:ring-purple-300 focus:outline-none focus:ring focus:ring-opacity-40"
          />
        </div>
        <div>
          <label for="password" class="block text-sm text-gray-800"
            >Password</label
          >
          <input
            v-model="password"
            name="password"
            type="password"
            class="block w-full px-4 py-2 mt-2 text-purple-700 bg-white border rounded-md focus:border-purple-400 focus:ring-purple-300 focus:outline-none focus:ring focus:ring-opacity-40"
          />
        </div>
        <div>
          <label for="password" class="block text-sm text-gray-800"
            >Password Confirm</label
          >
          <input
            v-model="password_confirmation"
            name="password_confirmation"
            type="password"
            class="block w-full px-4 py-2 mt-2 text-purple-700 bg-white border rounded-md focus:border-purple-400 focus:ring-purple-300 focus:outline-none focus:ring focus:ring-opacity-40"
          />
        </div>
        <div>
          <button
          class="btn btn-info"
          >
            Create Account
          </button>
        </div>
      </form>
      <p class="mt-8 text-xs font-light text-center text-gray-700">
        Don't have an account?

        <RouterLink
          to="/login"
          class="btn btn-success"
          >Login</RouterLink>

        
      </p>
    
    </div>


<div class="col-md-6"></div>

 
 </div>
  
</div>


  </div>
</template>