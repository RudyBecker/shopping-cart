<template>
  <div class="app">
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand>Microsoft Shopping Cart</b-navbar-brand>
      <b-navbar-nav class="ml-auto">
        <b-button variant="info" v-b-modal.shopping-cart
          ><b-icon icon="cart4"></b-icon>
          <span class="total-quantity ml-3"
            >Items: {{ totalQuantity }} Total: ${{ totalPrice }}</span
          ></b-button
        >
      </b-navbar-nav>
    </b-navbar>
    <section>
      <div class="d-flex justify-content-center">
        <div v-for="product in products" :key="product.id">
          <b-card
            :title="product.name"
            :img-src="product.image"
            :img-alt="product.name"
            img-top
            class="my-5 mx-5"
          >
            <b-card-text>
              <div>
                {{ product.description }}
              </div>
              <div>$ {{ product.price }}</div>
            </b-card-text>
            <span class="d-flex justify-content-center">
              <b-button @click="updateCart(product, 'subtract')" class="mx-2">
                -
              </b-button>
              <span class="pt-2"
                ><h5>{{ product.quantity }}</h5></span
              >
              <b-button @click="updateCart(product, 'add')" class="mx-2">
                +
              </b-button>
            </span>
          </b-card>
        </div>
      </div>
    </section>
    <div class="text-center">
      <b-button variant="info" v-b-modal.shopping-cart
        ><b-icon icon="cart4" class="mr-2"></b-icon>View Shopping Cart</b-button
      >
    </div>

    <div class="text-center mt-5">
      <h5>
        This demo website was coded by Rudy Becker.
        2020
      </h5>
    </div>

    <b-modal
      id="shopping-cart"
      centered
      title="Shopping Cart"
      :header-bg-variant="headerBgVariant"
      :header-text-variant="headerTextVariant"
    >
      <ul class="cart-dropdown__list">
        <li v-for="product in cart" :key="product.id">
          <div>{{ product.name }} ({{ product.quantity }})</div>
        </li>
      </ul>
      <div>Total: ${{ totalPrice }}</div>
    </b-modal>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [
        {
          id: 1,
          name: "Xbox Series X",
          image:
            "https://logos-download.com/wp-content/uploads/2016/02/Microsoft_logo_small.png",
          price: 399,
          description: "Microsoft Power Tools",
          quantity: 0,
        },
        {
          id: 2,
          name: "Office 365",
          image:
            "https://logos-download.com/wp-content/uploads/2016/02/Microsoft_logo_small.png",
          price: 199,
          description: "Microsoft Power Tools",
          quantity: 0,
        },
        {
          id: 3,
          name: "Bing",
          image:
            "https://logos-download.com/wp-content/uploads/2016/02/Microsoft_logo_small.png",
          price: 499,
          description: "Microsoft Power Tools",
          quantity: 0,
        },
      ],
      totalCost: "",
      headerBgVariant: "info",
      headerTextVariant: "light",
    };
  },

  computed: {
    cart() {
      return this.products.filter((product) => product.quantity > 0);
    },
    totalQuantity() {
      return this.products.reduce(
        (total, product) => total + product.quantity,
        0
      );
    },
    totalPrice() {
      let total = 0;
      this.products.forEach((item) => {
        total += item.price * item.quantity;
      });
      return total;
    },
  },
  methods: {
    updateCart(product, updateType) {
      for (let i = 0; i < this.products.length; i++) {
        if (this.products[i].id === product.id) {
          if (updateType === "subtract") {
            if (this.products[i].quantity !== 0) {
              this.products[i].quantity--;
            }
          } else {
            this.products[i].quantity++;
          }
          break;
        }
      }
    },
  },
};
</script>

<style></style>
