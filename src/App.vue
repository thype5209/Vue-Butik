<template>
  <main>
    <!-- Header -->
    <header class="bg-base-100 w-full border-b ">
      <div class="flex justify-between container mx-auto py-2">
        <div class=" flex flex-col sm:flex-row justify-start items-center gap-2 pl-5 sm:pl-0">
          <div class="flex items-center text-xs sm:text-sm gap-2">
            <font-awesome-icon :icon="['fas', 'envelope']" class="text-gray-800" />
            <span>Shop@gmail.com</span>
          </div>
          <span class="hidden md:block">|</span>
          <div class="flex items-center text-xs sm:text-sm gap-2">
            <font-awesome-icon :icon="['fas', 'phone']" class="text-gray-800" />
            <span>+62 8154651154</span>
          </div>
        </div>
        <router-link :to="{ name: 'login' }" v-if="loggedIn == false"
          class="auth flex flex-wrap gap-2 items-center text-xs sm:text-sm pr-4 sm:pr-0 cursor-pointer">
          <font-awesome-icon :icon="['fas', 'user']" />
          <span>Login</span>
        </router-link>
        <router-link :to="{ name: 'account.info' }" v-else
          class="auth flex flex-wrap gap-2 items-center text-xs sm:text-sm pr-4 sm:pr-0 cursor-pointer">
          <font-awesome-icon :icon="['fas', 'user']" />
          <span>{{ User.name }}</span>
        </router-link>
      </div>
    </header>
    <!-- End Header -->

    <!-- Logo And Form Search -->
    <section class="w-full bg-white sm:px-20 border-0 py-2 flex justify-between border-b">

      <!-- Logo -->
      <fieldset class=" hidden sm:block bg-primary rounded-lg px-2 py-1">
        <h1 class="text-xs sm:text-sm md:text-base lg:text-xl font-bold cursor-pointer text-white ">Shop-Butik</h1>
      </fieldset>
      <!-- End Logo -->

      <!-- Form Search -->
      <form action="#search" class="flex flex-row ">
        <input type="search" name="search" id="search"
          class="block w-full pl-4 text-sm text-gray-900 border border-gray-300 rounded-l-lg bg-gray-50 focus:ring-blue-500 focus:border-blue-500 "
          placeholder="search" />
        <button class="bg-primary text-white w-20 rounded-r-lg">Cari</button>
      </form>
      <!-- <div class="relative flex flex-row justify-center items-center group hover:text-primary gap-2">
        <font-awesome-icon :icon="['fas', 'heart']" class="text-gray-800 group-hover:text-primary transition-all" />
        <router-link :to="{ name: 'account.wishlist' }" class="capitalize relative font-semibold">Wishlist</router-link>
      </div> -->
      <!-- End Form Search -->
    </section>
    <!-- End Logo And Form Search -->

    <!-- Navigation Bar -->
    <nav class="bg-transparent md:py-2 px-0 sm:px-10 flex flex-wrap items-center justify-around">
      <!-- Dropdown Kategori -->
      <div class="dropdown block relative box-border w-max sm:w-40 h-full ">
        <!-- Button -->
        <button @click="dropdownShow" type="button" ref="dropdownNav"
          class="sm:px-2 px-1 py-2 sm:py-3 text-xs sm:text-base w-full h-full bg-primary group text-white font-bold  ">Semua
          Kategori
          <font-awesome-icon :icon="['fas', 'bars']"
            class="text-white group-hover:rotate-45 text-xs sm:text-base group-hover:text-primary transition ease-in" />
        </button>
        <!-- End Dropdown kategori -->

        <!-- List Dropdown -->
        <transition name="fade" v-show="showDropdown" @mouseup="showDropdown = false">
          <ul class="block shadow-md w-full absolute overflow-hidden bg-white z-[999]" v-closable="{
            exclude: ['dropdownNav'],
            handler: 'onClose'
          }">
            <li class="pl-4 py-2 group hover:bg-primary transition ease-in"><a
                class="text-sm md:text-base group-hover:text-white" href="#Baju">Baju</a></li>
            <li class="pl-4 py-2 group hover:bg-primary transition ease-in"><a
                class="text-sm md:text-base group-hover:text-white" href="#Kaos">Kaos</a></li>
            <li class="pl-4 py-2 group hover:bg-primary transition ease-in"><a
                class="text-sm md:text-base group-hover:text-white" href="#Celana">Celana</a></li>
            <li class="pl-4 py-2 group hover:bg-primary transition ease-in"><a
                class="text-sm md:text-base group-hover:text-white" href="#Fashion">Fashion</a></li>
          </ul>
        </transition>
        <!-- End List Dropdown -->
      </div>
      <!-- End Dropdown -->

      <!-- Navigation Router -->
      <ul class="inline-flex space-x-4 sm:space-x-10 md::space-x-24 border-b-2 pb-1 sm:border-b-0 sm:pb-0">
        <router-link :to="{ name: 'home' }" class="relative flex flex-row justify-center items-center group gap-2"
          :active-class="activeClass">
          <font-awesome-icon :icon="['fas', 'home']" class="transition-all" />
          <span class="capitalize relative font-semibold">Home</span>
        </router-link>
        <router-link :to="{ name: 'shop' }" class="relative flex flex-row justify-center items-center group gap-2"
          :active-class="activeClass">
          <font-awesome-icon :icon="['fas', 'shop']" class="transition-all" />
          <span class="capitalize relative font-semibold">Produk</span>
        </router-link>
        <router-link :to="{ name: 'about' }" class="relative flex flex-row justify-center items-center group gap-2"
          :active-class="activeClass">
          <font-awesome-icon :icon="['fas', 'user']" class="transition-all" />
          <span class="capitalize relative font-semibold">Tentang Kami</span>
        </router-link>
        <router-link :to="{ name: 'testimoni' }" class="relative flex flex-row justify-center items-center group gap-2"
          :active-class="activeClass">
          <font-awesome-icon :icon="['fas', 'comments']" class="transition-all" />
          <span class="capitalize relative font-semibold">Testimoni</span>
        </router-link>
      </ul>
      <!-- End Navigation -->

      <!-- Cart And Wishlist -->
      <div class="relative px-2 inline-flex space-x-4 justify-end">
        <router-link :to="{ name: 'cart' }"
          class="relative flex flex-row justify-center items-center group hover:text-primary gap-2"
          :active-class="activeClass">
          <font-awesome-icon :icon="['fas', 'cart-shopping']" class="transition-all" />
          <a href="#cart" class="capitalize relative font-semibold">Cart</a>
        </router-link>
      </div>
      <!-- Enda Cart And Wishlist -->

    </nav>

    <!-- End Navigation Bar -->


    <hr class="w-full h-3 bg-primary block">
    <!-- Content -->
    <router-view></router-view>
    <!-- End New Product -->


    <footer class="bg-white mt-20 border-t-2 border-primary">
      <div class="mx-auto w-full max-w-screen-xl p-4 py-6 lg:py-8">
        <div class="md:flex md:justify-between">
          <div class="mb-6 md:mb-0">
            <a href="https://flowbite.com/" class="flex items-center">
              <!-- <img src="https://flowbite.com/docs/images/logo.svg" class="h-8 mr-3" alt="FlowBite Logo" /> -->
              <span class="self-center text-2xl font-semibold whitespace-nowrap ">Shop Butik</span>
            </a>
          </div>
          <div class="grid grid-cols-2 gap-8 sm:gap-6 sm:grid-cols-3">
            <div>
              <h2 class="mb-6 text-sm font-semibold text-gray-900 uppercase ">Resources</h2>
              <ul class="text-gray-500 font-medium">
                <li class="mb-4">
                  <a href="https://flowbite.com/" class="hover:underline">Flowbite</a>
                </li>
                <li>
                  <a href="https://tailwindcss.com/" class="hover:underline">Tailwind CSS</a>
                </li>
              </ul>
            </div>
            <div>
              <h2 class="mb-6 text-sm font-semibold text-gray-900 uppercase ">Follow us</h2>
              <ul class="text-gray-500 font-medium">
                <li class="mb-4">
                  <a href="https://github.com/themesberg/flowbite" class="hover:underline ">Github</a>
                </li>
                <li>
                  <a href="https://discord.gg/4eeurUVvTy" class="hover:underline">Discord</a>
                </li>
              </ul>
            </div>
            <div>
              <h2 class="mb-6 text-sm font-semibold text-gray-900 uppercase ">Legal</h2>
              <ul class="text-gray-500 font-medium">
                <li class="mb-4">
                  <a href="#" class="hover:underline">Privacy Policy</a>
                </li>
                <li>
                  <a href="#" class="hover:underline">Terms &amp; Conditions</a>
                </li>
              </ul>
            </div>
          </div>
        </div>
        <hr class="my-6 border-gray-200 sm:mx-auto  lg:my-8" />
        <div class="sm:flex sm:items-center sm:justify-between">
          <span class="text-sm text-gray-500 sm:text-center">© 2023 <a href="https://flowbite.com/"
              class="hover:underline">ShopButik@</a>. All Rights Reserved.
          </span>
          <div class="flex mt-4 space-x-5 sm:justify-center sm:mt-0">
            <a href="#" class="text-gray-500 hover:text-gray-900">
              <svg class="w-4 h-4" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor"
                viewBox="0 0 8 19">
                <path fill-rule="evenodd"
                  d="M6.135 3H8V0H6.135a4.147 4.147 0 0 0-4.142 4.142V6H0v3h2v9.938h3V9h2.021l.592-3H5V3.591A.6.6 0 0 1 5.592 3h.543Z"
                  clip-rule="evenodd" />
              </svg>
              <span class="sr-only">Facebook page</span>
            </a>
            <a href="#" class="text-gray-500 hover:text-gray-900">
              <svg class="w-4 h-4" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor"
                viewBox="0 0 21 16">
                <path
                  d="M16.942 1.556a16.3 16.3 0 0 0-4.126-1.3 12.04 12.04 0 0 0-.529 1.1 15.175 15.175 0 0 0-4.573 0 11.585 11.585 0 0 0-.535-1.1 16.274 16.274 0 0 0-4.129 1.3A17.392 17.392 0 0 0 .182 13.218a15.785 15.785 0 0 0 4.963 2.521c.41-.564.773-1.16 1.084-1.785a10.63 10.63 0 0 1-1.706-.83c.143-.106.283-.217.418-.33a11.664 11.664 0 0 0 10.118 0c.137.113.277.224.418.33-.544.328-1.116.606-1.71.832a12.52 12.52 0 0 0 1.084 1.785 16.46 16.46 0 0 0 5.064-2.595 17.286 17.286 0 0 0-2.973-11.59ZM6.678 10.813a1.941 1.941 0 0 1-1.8-2.045 1.93 1.93 0 0 1 1.8-2.047 1.919 1.919 0 0 1 1.8 2.047 1.93 1.93 0 0 1-1.8 2.045Zm6.644 0a1.94 1.94 0 0 1-1.8-2.045 1.93 1.93 0 0 1 1.8-2.047 1.918 1.918 0 0 1 1.8 2.047 1.93 1.93 0 0 1-1.8 2.045Z" />
              </svg>
              <span class="sr-only">Discord community</span>
            </a>
            <a href="#" class="text-gray-500 hover:text-gray-900">
              <svg class="w-4 h-4" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor"
                viewBox="0 0 20 17">
                <path fill-rule="evenodd"
                  d="M20 1.892a8.178 8.178 0 0 1-2.355.635 4.074 4.074 0 0 0 1.8-2.235 8.344 8.344 0 0 1-2.605.98A4.13 4.13 0 0 0 13.85 0a4.068 4.068 0 0 0-4.1 4.038 4 4 0 0 0 .105.919A11.705 11.705 0 0 1 1.4.734a4.006 4.006 0 0 0 1.268 5.392 4.165 4.165 0 0 1-1.859-.5v.05A4.057 4.057 0 0 0 4.1 9.635a4.19 4.19 0 0 1-1.856.07 4.108 4.108 0 0 0 3.831 2.807A8.36 8.36 0 0 1 0 14.184 11.732 11.732 0 0 0 6.291 16 11.502 11.502 0 0 0 17.964 4.5c0-.177 0-.35-.012-.523A8.143 8.143 0 0 0 20 1.892Z"
                  clip-rule="evenodd" />
              </svg>
              <span class="sr-only">Twitter page</span>
            </a>
            <a href="#" class="text-gray-500 hover:text-gray-900">
              <svg class="w-4 h-4" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor"
                viewBox="0 0 20 20">
                <path fill-rule="evenodd"
                  d="M10 .333A9.911 9.911 0 0 0 6.866 19.65c.5.092.678-.215.678-.477 0-.237-.01-1.017-.014-1.845-2.757.6-3.338-1.169-3.338-1.169a2.627 2.627 0 0 0-1.1-1.451c-.9-.615.07-.6.07-.6a2.084 2.084 0 0 1 1.518 1.021 2.11 2.11 0 0 0 2.884.823c.044-.503.268-.973.63-1.325-2.2-.25-4.516-1.1-4.516-4.9A3.832 3.832 0 0 1 4.7 7.068a3.56 3.56 0 0 1 .095-2.623s.832-.266 2.726 1.016a9.409 9.409 0 0 1 4.962 0c1.89-1.282 2.717-1.016 2.717-1.016.366.83.402 1.768.1 2.623a3.827 3.827 0 0 1 1.02 2.659c0 3.807-2.319 4.644-4.525 4.889a2.366 2.366 0 0 1 .673 1.834c0 1.326-.012 2.394-.012 2.72 0 .263.18.572.681.475A9.911 9.911 0 0 0 10 .333Z"
                  clip-rule="evenodd" />
              </svg>
              <span class="sr-only">GitHub account</span>
            </a>
            <a href="#" class="text-gray-500 hover:text-gray-900">
              <svg class="w-4 h-4" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="currentColor"
                viewBox="0 0 20 20">
                <path fill-rule="evenodd"
                  d="M10 0a10 10 0 1 0 10 10A10.009 10.009 0 0 0 10 0Zm6.613 4.614a8.523 8.523 0 0 1 1.93 5.32 20.094 20.094 0 0 0-5.949-.274c-.059-.149-.122-.292-.184-.441a23.879 23.879 0 0 0-.566-1.239 11.41 11.41 0 0 0 4.769-3.366ZM8 1.707a8.821 8.821 0 0 1 2-.238 8.5 8.5 0 0 1 5.664 2.152 9.608 9.608 0 0 1-4.476 3.087A45.758 45.758 0 0 0 8 1.707ZM1.642 8.262a8.57 8.57 0 0 1 4.73-5.981A53.998 53.998 0 0 1 9.54 7.222a32.078 32.078 0 0 1-7.9 1.04h.002Zm2.01 7.46a8.51 8.51 0 0 1-2.2-5.707v-.262a31.64 31.64 0 0 0 8.777-1.219c.243.477.477.964.692 1.449-.114.032-.227.067-.336.1a13.569 13.569 0 0 0-6.942 5.636l.009.003ZM10 18.556a8.508 8.508 0 0 1-5.243-1.8 11.717 11.717 0 0 1 6.7-5.332.509.509 0 0 1 .055-.02 35.65 35.65 0 0 1 1.819 6.476 8.476 8.476 0 0 1-3.331.676Zm4.772-1.462A37.232 37.232 0 0 0 13.113 11a12.513 12.513 0 0 1 5.321.364 8.56 8.56 0 0 1-3.66 5.73h-.002Z"
                  clip-rule="evenodd" />
              </svg>
              <span class="sr-only">Dribbble account</span>
            </a>
          </div>
        </div>
      </div>
    </footer>

  </main>
</template>
<script >
import Katalog from './components/Katalog.vue';
import CarouselHeader from './components/CarouselHeader.vue';
import CarouselNewProduct from './components/CarouselNewProduct.vue';
import CarouselTerlaris from './components/CarouselTerlaris.vue';

import axios from 'axios';
export default {
  components: {
    Katalog,
    CarouselHeader,
    CarouselNewProduct,
    CarouselTerlaris,

  },

  data() {
    return {
      showDropdown: false,
      navbar: 'home',
      activeClass: 'text-primary transition-all',
      nonActiveClass: 'text-gray-800 hover:text-primary transition-all',
      User: [],
      access_token: localStorage.getItem('token'),
      loggedIn: localStorage.getItem('loggedIn'),
      CartLength: null,
      WishlistLenght: null,
      config: {
        cart: true,
        wishlist: true,
        user: true,
      },
      modalSearch: false,
      loadingPage: false,
    }
  },
  mounted() {
    if (this.loggedIn == "true" || this.loggedIn == true) {
      this.getUser()
    }
  },
  methods: {
    dropdownShow() {
      this.showDropdown = !this.showDropdown;
    },
    onClose() {
      this.showDropdown = false
    },
    getUser() {
      axios.get('//admin-enerel.delapain.com/api/user', {
        headers: { Authorization: 'Bearer ' + this.access_token }
      })
        .then(res => {
          this.User = res.data
          this.CartLength = res.data.cart.length;
          this.WishlistLenght = res.data.wishlist.length;
        }).catch(error => {
          const resError = error.response;
          console.log(error)
          if (resError.status === 401 && resError.statusText === "Unauthorized") {
            localStorage.removeItem('token')
            localStorage.removeItem('token_type')
            localStorage.setItem('loggedIn', false);
          }
        })
    },
  }
}
</script>
<style>
.fade-enter-active,
.fade-leave-active {
  transition: height 1s ease-in-out;
  overflow: hidden;
}

.fade-enter-from,
.fade-leave-to {
  height: 0;
}
</style>
