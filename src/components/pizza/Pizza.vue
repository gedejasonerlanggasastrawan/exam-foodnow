<template>
    <div class="container d-flex flex-wrap justify-content-center py-5">
      <!-- Section: Choose Your Pizza -->
      <div>
        <div class="row col-12">
          <h2 class="fw-bold mb-4 text-center text-md-start" style="color: #e77e23;">Choose your pizza</h2>
          <!-- Pizza Card -->
          <div class="col-sm-6 col-lg-4 mb-4 d-flex justify-content-center" v-for="pizza in pizzas" :key="pizza.id">
            <button
              class="card interactive-card position-relative"
              :class="{ 'selected-pizza': selectedPizza?.id === pizza.id }"
              style="width: auto; height: auto;"
              @click="selectPizza(pizza)"
            >
              <!-- Badge OFFER -->
              <img
                v-if="pizza.discount.is_active"
                src="@/assets/img/ribbon.svg"
                alt="Offer"
                class="position-absolute top-0 end-0"
                style="width: 40%;"
              />
              <!-- Pizza Content -->
              <div class="row g-0 align-items-center h-100">
                <div class="col-12 col-md-6 d-flex justify-content-center align-items-center">
                  <img
                    :src="pizza.image"
                    class="img-fluid rotating-img"
                    :alt="pizza.name"
                  />
                </div>
                <div class="col-12 col-md-6 d-flex justify-content-center align-items-center">
                  <div class="card-body text-center text-md-start">
                    <h5 class="card-title fw-bold">{{ pizza.name }}</h5>
                    <p class="card-text">
                      <!-- Harga dengan diskon -->
                      <span v-if="pizza.discount.is_active">
                        ${{ pizza.discount.final_price }}
                      </span>
                      <!-- Harga asli -->
                      <span
                        v-if="pizza.discount.is_active"
                        class="text-muted text-decoration-line-through ms-1"
                      >
                        ${{ pizza.price }}
                      </span>
                      <!-- Harga tanpa diskon -->
                      <span v-else>${{ pizza.price }}</span>
                    </p>
                  </div>
                </div>
              </div>
            </button>
          </div>
        </div>
  
        <!-- Section: Custom Pizza -->
        <div class="col-12 py-5">
          <h2 class="fw-bold mt-5 mb-4 text-center text-md-start" style="color: #e77e23;">
            Custom Pizza
          </h2>
          <!-- Size Options -->
          <div class="mb-4">
            <h4 class="fw-bold my-3">Size</h4>
            <div class="form-check form-check-inline" v-for="size in sizes" :key="size.id">
              <input
                class="form-check-input"
                type="radio"
                :id="`size${size.name}`"
                :value="size"
                v-model="selectedSize"
                :disabled="!selectedPizza"
              />
              <label class="form-check-label" :for="`size${size.name}`">
                {{ size.name }}
                <span v-if="size.extra_price" style="opacity: 50%;">
                  (+${{ size.extra_price }})
                </span>
              </label>
            </div>
          </div>
  
          <!-- Toppings Options -->
          <div class="mb-4 col-12">
            <h4 class="fw-bold my-3">Toppings</h4>
            <div class="d-flex flex-wrap justify-content-center justify-content-md-start">
              <div
                v-for="topping in allToppings"
                :key="topping.id"
                class="topping-checkbox-wrapper me-3 mb-2"
                :class="{ 'disabled-topping': !selectedPizza }"
              >
                <input
                  type="checkbox"
                  :id="`topping-${topping.id}`"
                  :value="topping.id"
                  :disabled="selectedPizza && !availableToppings.includes(topping.id)"
                  v-model="selectedToppings"
                  class="topping-checkbox"
                />
                <label
                 :for="`topping-${topping.id}`"
                  class="topping-label"
                  :class="{
                    'disabled-topping': selectedPizza && !availableToppings.includes(topping.id)
                  }"
                >
                  {{ topping.name }}
                </label>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { reactive, ref, computed, watch } from "vue";
  import pizzasRaw from "@/assets/json/pizza-list.json";
  import toppingsRaw from "@/assets/json/topping-list.json";
  import sizesRaw from "@/assets/json/size-list.json";
  
  const pizzas = reactive(pizzasRaw.data);
  const allToppings = reactive(toppingsRaw.data);
  const sizes = reactive(sizesRaw.data);
  
  const selectedPizza = ref(null);
  const selectedSize = ref(null); // Tidak ada ukuran yang dipilih secara default
  const selectedToppings = ref([]);
  
  // Fungsi untuk emit data ke komponen induk
  const emit = defineEmits(["selectPizza", "selectSize", "selectToppings"]);
  
  // Fungsi memilih pizza
  const selectPizza = (pizza) => {
    selectedPizza.value = pizza;
    selectedSize.value = [];
    selectedToppings.value = []; // Reset topping jika mengganti pizza
    emit("selectPizza", pizza.id); // Emit ID pizza yang dipilih
  };
  
  // Emit ukuran saat berubah
  watch(selectedSize, (newSize) => {
    emit("selectSize", newSize.id); // Emit ID ukuran
  });
  
  // Emit topping saat berubah
  watch(selectedToppings, (newToppings) => {
    emit("selectToppings", newToppings); // Emit array ID topping
  });
  
  // Topping yang tersedia untuk pizza terpilih
  const availableToppings = computed(() => {
    if (!selectedPizza.value) return allToppings.map((t) => t.id);
    return selectedPizza.value.toppings;
  });
  </script>
  
  
  <style scoped>
  .selected-pizza {
    background-color: #e77e23 !important; /* Warna latar belakang oranye */
    color: white !important; /* Teks menjadi putih */
    border: none;
    transform: scale(1.03); /* Efek zoom kecil */
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15); /* Tambahkan bayangan */
  }
  
  .selected-pizza .rotating-img {
    transform: rotate(10deg) scale(1.05);
  }
  
  .btn-outline-warning {
    color: #e77e23;
    border: 1px solid #e77e23;
  }
  
  .btn-outline-warning:hover {
    background-color: #e77e23;
    color: white;
  }
  
  /* Checkbox Toppings Styling */
  .topping-checkbox-wrapper {
    display: inline-block;
  }
  
  .topping-checkbox {
    display: none; /* Hide the checkbox itself */
  }
  
  .topping-label {
    text-align: center;
    width: 100px;
    display: inline-block;
    padding: 8px 16px;
    border: 1px solid black; /* Warna border abu-abu terang */
    border-radius: 20px;
    color: black; /* Teks abu-abu gelap */
    font-weight: bold; /* Teks tebal */
    cursor: pointer;
    transition: all 0.3s ease;
  }
  
  .topping-checkbox:checked + .topping-label {
    background-color: #f8d8bd; /* Warna oranye ketika dipilih */
    color: #e77e23; /* Teks putih ketika dipilih */
    border: 1px solid #e77e23;
  }
  
  .topping-label:hover {
    color: #e77e23; /* Sedikit efek hover dengan warna oranye */
    border: 1px solid #e77e23;
  }
  
  .disabled-topping {
    opacity: 0.5;
    pointer-events: none;
  }
  
  .card {
    border-radius: 10px;
    position: relative;
  }
  
  .card-img-top {
    margin-top: 20px;
  }
  
  .card-body {
    padding-top: 10px;
    text-align: left;
  }
  
  .card-link {
    text-decoration: none;
    color: inherit;
  }
  
  .interactive-card {
    width: 300px; /* Atur sesuai kebutuhan */
    max-width: auto;
    padding: 10%;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    cursor: pointer;
  }
  
  .interactive-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 15px rgba(0, 0, 0, 0.2);
    background-color: #f8d8bd;
  }
  
  .interactive-card:active {
    transform: scale(0.98);
    box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
  }
  
  .rotating-img {
    transition: transform 0.4s ease-in-out;
  }
  
  .card:hover .rotating-img {
    transform: rotate(10deg) scale(1.05);
  }
  
  
  h5, h4, p, label, button {
    font-size: small;
  }
  
  .form-check-input {
    transition: all 0.3s ease; /* Animasi untuk hover dan active */
  }
  
  /* Hover style untuk checkbox */
  .form-check-input:hover {
    background-color: #f5d6a0;
    border-color: #e77e23;
    box-shadow: 0 0 5px rgba(231, 126, 35, 0.5);
  }
  
  /* Active style untuk checkbox */
  .form-check-input:active {
    background-color: #e77e23;
    border-color: #b3651c;
    box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.3);
  }
  
  /* Checked style tetap sama */
  .form-check-input:checked {
    background-color: #e77e23;
    border-color: #e77e23;
    box-shadow: 0 0 5px rgba(231, 126, 35, 0.5);
  }
  
  .container {
    max-width: 1200px; /* Sesuaikan dengan kebutuhan */
  }
  
  .row {
    margin: 0 auto; /* Pusatkan row */
  }
  
  @media (max-width: 768px) {
    .interactive-card {
      margin-bottom: 20px;
      width: 90%; /* Sesuaikan dengan layar kecil */
    }
    
    .rotating-img {
      width: 60% !important;
    }
    .card-body {
      text-align: center !important;
    }
    .interactive-card {
      margin-bottom: 20px;
    }
  }
  
  @media (max-width: 576px) {
    .rotating-img {
      width: 50% !important;
    }
    .interactive-card {
      margin-bottom: 20px;
    }
  }
  </style>