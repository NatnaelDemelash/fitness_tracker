<template>
  <div class="px-4 py-10 max-w-screen-md mx-auto">
    <!-- Status Message -->
    <div
      v-if="statusMsg || errMsg"
      class="bg-light-grey p-4 shadow-lg rounded-md"
    >
      <p class="text-dark-blue">{{ statusMsg }}</p>
      <p class="text-red-500">{{ errMsg }}</p>
    </div>

    <!-- Create -->
    <div class="p-8 flex item-start bg-light-grey rounded-md shadow-lg">
      <!-- form -->
      <form class="flex flex-col gap-y-5 w-full">
        <h1 class="text-3xl text-deep-orange">Create Exersise</h1>
        <!-- workoutName -->
        <div class="flex flex-col">
          <label
            for="workout-name"
            class="mb-1 text-md text-dar
          "
            >Workout Name</label
          >
          <input
            type="text"
            required
            class="p-2 text-gray-500 focus:outline-none "
            v-model="workoutName"
            id="workout-name"
          />
        </div>

        <!-- Workout Type -->
        <div class="flex flex-col">
          <label
            for="workout-type"
            class="mb-1 text-md text-dar
          "
            >Workout Type</label
          >

          <select
            id="workout-type"
            v-model="workoutType"
            class="p-2 text-gray-500 focus:outline-none "
          >
            <option value="select-type">Select Type</option>
            <option value="strength">Muscular/Strength</option>
            <option value="cardio">Endurance/Cardio</option>
          </select>
        </div>

        <!-- Strength Training Inputs -->

        <div v-if="workoutType === 'strength'" class="flex flex-col gap-y-4">
          <div
            class="flex flex-col gap-x-6 relative md:flex-row"
            v-for="(item, index) in exercises"
            :key="index"
          >
            <div class="flex flex-col md:w-1/3">
              <label for="exersise-name" class="mb-1 text-md text-dark-blue">
                Exersise
              </label>
              <input
                type="text"
                class="w-full p-2 text-gray-500 focus:outline-none"
                v-model="item.exercise"
              />
            </div>

            <div class="flex flex-col flex-1">
              <label for="sets" class="mb-1 text-md text-dark-blue">
                Sets
              </label>
              <input
                type="text"
                class="w-full p-2 text-gray-500 focus:outline-none"
                v-model="item.sets"
              />
            </div>

            <div class="flex flex-col flex-1">
              <label for="reps" class="mb-1 text-md text-dark-blue">
                Reps
              </label>
              <input
                type="text"
                class="w-full p-2 text-gray-500 focus:outline-none"
                v-model="item.reps"
              />
            </div>

            <div class="flex flex-col flex-1">
              <label for="weight" class="mb-1 text-md text-dark-blue">
                Weight(KG's)
              </label>
              <input
                type="text"
                class="w-full p-2 text-gray-500 focus:outline-none"
                v-model="item.weight"
              />
            </div>

            <img
              src="../assets/images/trash-light-green.png"
              alt=""
              class="h-4 w-auto absolute -left-5 cursor-pointer"
            />
          </div>
          <button
            type="button"
            class="mt-6 mx-auto py-2 px-10 rounded-full self-start text-md text-white bg-dark-blue duration-200 border-solid border-2 border-transparent  hover:bg-deep-orange hover:text-white"
          >
            Add Exersise
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "create",
  setup() {
    // Create data
    const workoutName = ref("");
    const workoutType = ref("Select workout Type");
    const exercises = ref([1]);
    const statusMsg = ref(null);
    const errMsg = ref(null);
    // Add exercise

    // Delete exercise

    // Listens for chaging of workout type input

    // Create workout

    return { workoutName, workoutType, exercises, statusMsg, errMsg };
  },
};
</script>
