<template>
  <div class="max-w-screen-sm mx-auto px-4 py-10">
    <!-- Error Handiling -->
    <div v-if="errMsg" class="mb-10 rounded p-4 bg-light-grey shadow-lg">
      <p class="text-red-500">{{ errMsg }}</p>
    </div>

    <!-- Login form -->
    <form
      @submit.prevent="login"
      class="p-8 flex flex-col bg-light-grey rounded-md shadow-lg"
    >
      <h1 class="text-3xl font-bold text-deep-orange uppercase mb-4">
        Login
      </h1>

      <div class="flex flex-col mb-2">
        <label for="email" class="text-small  text-dark-blue mb-1">Email</label>
        <input
          type="text"
          class="p-2  text-gray-500 focus:outline-none"
          id="email"
          v-model="email"
          required
        />
      </div>

      <div class="flex flex-col mb-2">
        <label for="password" class="text-small  text-dark-blue mb-1"
          >Password</label
        >
        <input
          type="password"
          class="p-2  text-gray-500 focus:outline-none"
          id="password"
          v-model="password"
          required
        />
      </div>

      <button
        type="submit"
        class="mt-6 mx-auto py-2 px-10 rounded-full self-start text-md text-white bg-dark-blue duration-200 border-solid border-2 border-transparent  hover:bg-deep-orange hover:text-white"
      >
        Login
      </button>

      <router-link class="text-md mt-6 text-center" :to="{ name: 'Register' }">
        Don't have an account?
        <span class="text-deep-orange uppercase font-bold">Register</span>
      </router-link>
    </form>
  </div>
</template>

<script>
import { ref } from "vue";
import { useRouter } from "vue-router";
import { supabase } from "../supabase/supabase";
export default {
  name: "Login",
  setup() {
    // Create data / vars
    const router = useRouter();
    const email = ref(null);
    const password = ref(null);
    const errMsg = ref(null);

    // Login function
    const login = async () => {
      try {
        const { error } = await supabase.auth.signIn({
          email: email.value,
          password: password.value,
        });
        if (error) throw error;
        router.push({ name: "Home" });

        return;
      } catch (error) {
        errMsg.value = `Error : ${error.message}`;
        setTimeout(() => {
          errMsg.value = null;
        }, 5000);
      }
    };
    return { email, password, errMsg, login };
  },
};
</script>
