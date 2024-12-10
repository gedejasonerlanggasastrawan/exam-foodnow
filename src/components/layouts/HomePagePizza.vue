<template>
    <div class="container align-items-center my-5">
      <div class="row">
        <!-- Komponen Pizza -->
        <div class="col-12 col-lg-9">
          <pizza
            @selectPizza="handlePizzaSelection"
            @selectSize="handleSizeSelection"
            @selectToppings="handleToppingSelection"
          ></pizza>
        </div>
  
        <!-- Payment Summary -->
        <div
          class="col-12 col-lg-3 mt-4"
        >
          <div class="card p-4 sticky-top" style="height: fit-content;">
            <h5 class="fw-bold mb-4" style="color: #e77e23;">Payment Summary</h5>
            <ul class="list-unstyled">
              <!-- Pizza -->
              <li>
                {{ selectedPizza.name || 'Select a Pizza' }}
                <span class="float-end">
                  ${{ selectedPizza.discount?.is_active ? selectedPizza.discount.final_price : selectedPizza.price }}
                </span>
              </li>
              <!-- Size -->
              <li>
                Size - {{ selectedSize.name || 'Select Size' }}
                <span class="float-end">${{ selectedSize.extra_price || 0 }}</span>
              </li>
              <!-- Toppings -->
              <li v-for="topping in orderedToppings" :key="topping.id">
                {{ topping.name }}
                <span class="float-end">${{ topping.price }}</span>
              </li>
            </ul>
            <hr>
            <!-- Total Price -->
            <div class="d-flex justify-content-between fw-bold">
              <span>Total Price</span>
              <span style="color: #e77e23;">${{ calculateTotalPrice() }}</span>
            </div>
            <!-- Tombol Order Now -->
            <button
              class="btn mt-4 btnclick w-100"
              style="color: white; border-radius: 50px;"
              @click="showModal = true"
              :disabled="isOrderDisabled"
            >
              Order Now
            </button>
          </div>
        </div>
      </div>
  
      <!-- Modal Order Success -->
      <div v-if="showModal" class="modal-overlay">
        <div class="modal-content">
          <img
            src="@/assets/img/pizza.gif"
            alt="Credit Card"
            class="modal-image"
          />
          <h4>Order Success</h4>
          <p>Thank you, we have received your order successfully.</p>
          <button
            class="btn btnclick"
            @click="showModal = false"
            style="color: white; border-radius: 50px;"
          >
            Close
          </button>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from "vue";
  import pizzasRaw from "@/assets/json/pizza-list.json";
  import toppingsRaw from "@/assets/json/topping-list.json";
  import sizesRaw from "@/assets/json/size-list.json";
  import Pizza from '../pizza/Pizza.vue';
  
  const selectedPizza = ref({});
  const selectedSize = ref({});
  const selectedToppingIds = ref([]); // Melacak ID topping sesuai urutan klik
  const showModal = ref(false);  // Untuk kontrol modal
  
  // Handlers untuk pilihan
  const handlePizzaSelection = (pizzaId) => {
    // Reset size and toppings
    selectedSize.value = {};          // Reset size
    selectedToppingIds.value = [];    // Reset toppings
  
    // Set the selected pizza
    selectedPizza.value = pizzasRaw.data.find((pizza) => pizza.id === pizzaId) || {};
  };
  
  const handleSizeSelection = (sizeId) => {
    selectedSize.value = sizesRaw.data.find((size) => size.id === sizeId) || {};
  };
  
  const handleToppingSelection = (toppingIds) => {
    // Tambahkan topping ID ke dalam array sesuai dengan urutan klik
    toppingIds.forEach((id) => {
      if (!selectedToppingIds.value.includes(id)) {
        selectedToppingIds.value.push(id);
      }
    });
  };
  
  // Ordered toppings berdasarkan ID yang diurutkan
  const orderedToppings = computed(() => {
    return selectedToppingIds.value.map((id) =>
      toppingsRaw.data.find((topping) => topping.id === id)
    ).filter(Boolean); // Filter untuk memastikan data valid
  });
  
  // Kalkulasi total harga
  const calculateTotalPrice = () => {
    const pizzaPrice = selectedPizza.value.discount?.is_active
      ? selectedPizza.value.discount.final_price
      : selectedPizza.value.price || 0;
    const sizePrice = selectedSize.value.extra_price || 0;
    const toppingsPrice = orderedToppings.value.reduce((total, topping) => total + topping.price, 0);
  
    return pizzaPrice + sizePrice + toppingsPrice;
  };
  
  // Cek apakah tombol order harus disabled
  const isOrderDisabled = computed(() => {
    return !selectedPizza.value.id || !selectedSize.value.id || selectedToppingIds.value.length === 0;
  });
  </script>
  
  <style scoped>
  .modal-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.5);
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 2000;
  }
  
  .modal-content {
      background-color: white;
      padding: 2rem;
      border-radius: 8px;
      width: 300px;
      text-align: center;
  }
  
  .modal-content h4 {
      margin-bottom: 1rem;
  }
  
  .modal-content p {
      margin-bottom: 2rem;
  }
  
  .modal-image {
      display: block;
      margin: 0 auto;
      width: 50%;
  }
  
  .btnclick {
      background-color: #e77e23;
  }
  
  .btnclick:hover {
      background-color: #c16515;
  }
  </style>