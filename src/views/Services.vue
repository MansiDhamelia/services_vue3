<template>
  <div class="min-h-screen flex justify-center items-center">
    <div class="box-content w-1/2 bg-gray-700 rounded-xl">
      <h1 class="from-neutral-400 text-6xl py-9 text-gray-50">Services</h1>

      <div
        class="flex flex-col justify-between bottom-4 mx-12 p-2 items-center"
      >
        <div
          class="
            flex
            justify-between
            items-start
            w-full
            bg-gray-300
            p-6
            border-b
            cursor-pointer
          "
          @click="get(index)"
          v-for="(service, index) in services"
          :key="index"
          :style="isActive(index)"
        >
          <p class="font-semibold text-xl">{{ service.name }}</p>
          <p id="price1" class="font-semibold text-xl">
            ${{ service.price }}.00
          </p>
        </div>
        <div
          class="flex justify-between items-start mb-3 w-full p-6 border-b"
          id="totalId"
        >
          <p class="text-white text-lg">Total:</p>
          <p class="text-white text-lg" id="totalAmount">
            ${{ result || 0.0 }}.00
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, reactive, computed } from "vue";

export default {
  components: {},
  setup() {
    const services = reactive([
      {
        name: "Web Development",
        price: 300,
        isActive: false,
      },
      {
        name: "Design",
        price: 400,
        isActive: false,
      },
      {
        name: "Integration",
        price: 250,
        isActive: false,
      },
      {
        name: "Training",
        price: 220,
        isActive: false,
      },
    ]);
    const result = computed(() => {
      let total = 0;
      services.filter((e) => {
        if (e.isActive) {
          total += e.price;
        }
      });
      return total;
    });
    function isActive(index) {
      return {
        backgroundColor: this.services[index].isActive ? "lightyellow" : "",
      };
    }
    function get(index) {
      this.services[index].isActive = !this.services[index].isActive;
    }
    return {
      services,
      isActive,
      get,
      result,
    };
  },
};
</script>
