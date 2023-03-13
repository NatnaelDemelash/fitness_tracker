<template>
  <div class="max-w-screen-sm mx-auto px-4 py-10">
    <!-- Error Handiling -->
    <div v-if="errMsg" class="mb-10 rounded p-4 bg-light-grey shadow-lg">
      <p class="text-red-500">{{ errMsg }}</p>
    </div>

    <!-- Registration form -->
    <form
      @submit.prevent="register"
      class="p-8 flex flex-col bg-light-grey rounded-md shadow-lg"
    >
      <h1 class="text-3xl font-bold text-deep-orange uppercase mb-4">
        Register
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

      <div class="flex flex-col mb-2">
        <label for="confirmPassword" class="text-small  text-dark-blue mb-1"
          >Confirm Password</label
        >
        <input
          type="password"
          class="p-2 text-gray-500 focus:outline-none "
          id="confirmPassword"
          v-model="confirmPassword"
          required
        />
      </div>

      <button
        type="submit"
        class="mt-6 mx-auto py-2 px-10 rounded-full self-start text-md text-white bg-dark-blue duration-200 border-solid border-2 border-transparent  hover:bg-deep-orange hover:text-white"
      >
        Register
      </button>

      <router-link class="text-md mt-6 text-center" :to="{ name: 'Login' }">
        Already have an account?
        <span class="text-deep-orange uppercase font-bold">Login</span>
      </router-link>
    </form>
  </div>
</template>

<script>
import { ref } from "vue";
import { useRouter } from "vue-router";
import { supabase } from "../supabase/supabase";
export default {
  name: "register",
  setup() {
    // Create data / vars
    const router = useRouter();
    const email = ref(null);
    const password = ref(null);
    const confirmPassword = ref(null);
    const errMsg = ref(null);

    // Register function
    const register = async () => {
      if (password.value === confirmPassword.value) {
        try {
          const { error } = await supabase.auth.signUp({
            email: email.value,
            password: password.value,
          });
          if (error) throw error;
          router.push({ name: "Login" });
        } catch (error) {
          errMsg.value = error.message;
          setTimeout(() => {
            errMsg.value = null;
          }, 5000);
        }
        return;
      }
      errMsg.value = "Error: Password does not match!";
      setTimeout(() => {
        errMsg.value = null;
      }, 5000);
    };

    return { email, password, confirmPassword, errMsg, register };
  },
};
</script>
