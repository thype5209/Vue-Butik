<template>
    <div class="container mx-auto">
        <!-- breadcrumb -->
        <div class="container py-4 flex items-center gap-3">
            <router-link to="/" class="text-primary text-base">
                <i class="fa-solid fa-house"></i>
            </router-link>
            <span class="text-sm text-gray-400">
                <i class="fa-solid fa-chevron-right"></i>
            </span>
            <p class="text-gray-600 font-medium">Cart</p>
        </div>
        <!-- ./breadcrumb -->

        <!-- Wrapper -->
        <div class="container grid grid-cols-1 md:grid-cols-12 items-start gap-4 pt-4 pb-16">
            <div class="col-span-5 bg-transparent">
                <div class="grid grid-cols-3 justify-items-center items-center border gap-6 p-4 border-gray-200 rounded"
                    v-for="(item, index) in Cart" :key="item.id" :index="index">
                    <div class="w-28" v-if="item.product.galleriesdefault != null">
                        <img :src="item.product.galleriesdefault.photo" alt="product 6" class="w-full">
                    </div>
                    <div class="w-1/3 flex flex-col">
                        <h2 class="text-gray-800 text-sm font-medium uppercase whitespace-nowrap">{{ item.product.name }}
                        </h2>
                        <p class="text-gray-800 text-xs font-extralight whitespace-nowrap">Jumlah : {{
                            item.quantity }}</p>
                    </div>
                    <div class="text-primary text-sm font-semibold">{{ rupiah(item.price) }}</div>
                </div>
                <dl class="max-w-full text-gray-900 divide-y divide-gray-200 dark:text-white dark:divide-gray-700 p-4">
                    <div class="flex flex-row pb-3 justify-between">
                        <dt class="mb-1 text-gray-500 text-lg dark:text-gray-400">Sub Total</dt>
                        <dd class="text-lg font-semibold text-black">{{ rupiah(subtotal) }}</dd>
                    </div>
                    <div class="flex flex-row pb-3 justify-between">
                        <dt class="mb-1 text-gray-500 text-lg dark:text-gray-400">Estimasi Waktu Pembayaran</dt>
                        <dd class="text-lg font-semibold text-black">{{ waktuTersisa }}</dd>
                    </div>
                </dl>
            </div>
            <div class="col-span-7  pb-5 pt-2 px-8 border flex flex-col justify-center items-start">
                <form @submit.prevent="submit" class="  w-full h-full">
                    <div class="grid grid-cols-2 space-y-4">
                        <div class=" col-span-2">
                            <label for="dropzone-file" v-if="file == null"
                                class="flex flex-col items-center justify-center w-full h-64 border-2 border-gray-300 border-dashed rounded-lg cursor-pointer bg-gray-50 dark:hover:bg-bray-800 dark:bg-gray-700 hover:bg-gray-100 dark:border-gray-600 dark:hover:border-gray-500 dark:hover:bg-gray-600">
                                <div class="flex flex-col items-center justify-center pt-5 pb-6">
                                    <svg aria-hidden="true" class="w-10 h-10 mb-3 text-gray-400" fill="none"
                                        stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                            d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12">
                                        </path>
                                    </svg>
                                    <p class="mb-2 text-sm text-gray-500 dark:text-gray-400"><span
                                            class="font-semibold">Klik Untuk Upload Bukti Bayar</span> or drag and drop</p>
                                    <p class="text-xs text-gray-500 dark:text-gray-400">SVG, PNG, JPG or GIF
                                        (MAX. 800x400px)</p>
                                </div>
                                <input id="dropzone-file" @change="fileSelected($event)" type="file" class="hidden"
                                    name="file" />
                            </label>
                            <div v-else class=" p-2 border border-primary">
                                <img :src="URLFile" alt="Image" class="w-full h-full object-cover">
                            </div>
                        </div>
                        <div class="col-span-1 px-3 md:px-8">
                            <div class="flex flex-col">
                                <label for="nama"
                                    class="block mb-2 text-sm font-medium text-gray-900 capitalize">Nama</label>
                                <input type="text" v-model="name"
                                    class="focus:ring-primary focus:border-primary rounded-lg block text-sm border px-2 py-1"
                                    placeholder="Masukkan Nama">
                            </div>
                        </div>
                        <div class="col-span-1 px-3 md:px-8">
                            <div class="flex flex-col">
                                <label for="email"
                                    class="block mb-2 text-sm font-medium text-gray-900 capitalize">Email</label>
                                <input type="email" v-model="email"
                                    class="focus:ring-primary focus:border-primary rounded-lg block text-sm border px-2 py-1"
                                    placeholder="@gmail.com">
                            </div>
                        </div>
                        <div class="col-span-1 px-3 md:px-8">
                            <div class="flex flex-col">
                                <label for="No.HP"
                                    class="block mb-2 text-sm font-medium text-gray-900 capitalize">No.HP</label>
                                <input type="tel" v-model="phoneNumber"
                                    class="focus:ring-primary focus:border-primary rounded-lg block text-sm border px-2 py-1"
                                    placeholder="+62">
                            </div>
                        </div>
                        <div class="col-span-1 px-3 md:px-8">
                            <div class="flex flex-col">
                                <label for="Alamat"
                                    class="block mb-2 text-sm font-medium text-gray-900 capitalize">Alamat</label>
                                <input type="text" v-model="address"
                                    class="focus:ring-primary focus:border-primary rounded-lg block text-sm border px-2 py-1"
                                    placeholder="@.......">
                            </div>
                        </div>
                        <div class="col-span-2">
                            <button type="submit"
                                class="bg-primary rounded-lg text-lg text-white text-center px-4 py-2 w-full border-2 border-primary hover:bg-transparent hover:text-primary transition-all">Lanjutkan</button>
                        </div>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script>
import CryptoJS from 'crypto-js';
import axios from 'axios';
import Swal from 'sweetalert2';

export default {
    data() {
        return {
            encCart: localStorage.getItem('cart'),
            encQuantityItem: localStorage.getItem('quantityItem'),
            subtotal: localStorage.getItem('subtotal'),
            Cart: [],
            quantityItem: [],
            access_token: localStorage.getItem('token'),
            loggedIn: localStorage.getItem('loggedIn'),
            name: "wawan",
            email: "wawan@gmail.com",
            phoneNumber: '08152469845',
            address: 'Jl. Pendidikan',
            file: null,
            URLFile: null,
            estimasi: Number(localStorage.getItem('estimasi')),
            waktuTersisa: null,
        }
    },
    mounted() {
        const decryptedCart = CryptoJS.AES.decrypt(this.encCart, '12')
        const parseJSON = JSON.parse(decryptedCart.toString(CryptoJS.enc.Utf8));
        const decryptedQuantityItem = CryptoJS.AES.decrypt(this.encQuantityItem, '12')
        const parseJSONQuantityItem = JSON.parse(decryptedQuantityItem.toString(CryptoJS.enc.Utf8));
        this.Cart = parseJSON;
        this.quantityItem = parseJSONQuantityItem;
        for (let i = 0; i < this.Cart.length; i++) {
            const element = this.Cart[i];
            element.price = this.quantityItem[i].price
            element.quantity = this.quantityItem[i].quantity
        }
        try {
            this.tampilkanWaktuTersisa(this.estimasi); // ID elemen HTML yang akan menampilkan waktu tersisa adalah "waktuTersisa"
        } catch (error) {
            console.error(error.message);
        }

    },
    methods: {
        hitungWaktuTersisa(menit) {
            if (isNaN(menit)) {
                throw new Error("Input harus berupa angka");
            }

            if (menit <= 0) {
                throw new Error("Input harus lebih besar dari 0");
            }

            if (menit > 10) {
                
                throw new Error("Proses pembayaran melebihi batas waktu yang ditentukan");
                
            }
            if(this.estimasi == 0 || this.estimasi < 1){
                localStorage.removeItem('cart');
                localStorage.removeItem('subtotal');
                localStorage.removeItem('quantityItem');
                localStorage.removeItem('estimasi');
                this.$router.push({name: 'cart'})
            }

            return menit;
        },
        tampilkanWaktuTersisa(menit) {
            try {
                let waktuTersisa = this.hitungWaktuTersisa(menit);
                let jam = Math.floor(waktuTersisa / 60);
                let sisaMenit = waktuTersisa % 60;

                if (jam > 0) {
                    this.waktuTersisa = jam + " jam " + sisaMenit + " menit";
                } else {
                    this.waktuTersisa = sisaMenit + " menit";
                    localStorage.setItem('estimasi', sisaMenit)

                }

                if (waktuTersisa > 0) {
                    setTimeout(() => {
                        this.tampilkanWaktuTersisa(waktuTersisa - 1);
                        console.log(waktuTersisa)
                    }, 60000); // Mengulang fungsi setiap 1 menit (60.000 milidetik)
                }
            } catch (error) {
                console.error(error.message);
            }
        },
        rupiah(number) {
            return new Intl.NumberFormat("id-ID", {
                style: "currency",
                currency: "IDR"
            }).format(number);
        },
        fileSelected(e) {
            this.file = e.target.files[0];
            this.URLFile = URL.createObjectURL(e.target.files[0])
            console.log(this.file)
        },
        submit() {
            let idProduk = this.Cart.map((item) => {
                return item.product_id
            })
            if (this.file == null) {
                Swal.fire({
                    title: "Bukti Transaksi Kosong",
                    text: 'Harap Bukti Transaksi Di Isi Untuk Melanjutkan',
                    confirmButtonText: 'Keluar',
                })
            } else {
                axios.get('//admin-enerel.delapain.com/api/user', {
                    headers: { Authorization: 'Bearer ' + this.access_token }
                }).then((res) => {
                    const data = {
                        user_id: res.data.id,
                        name: this.name,
                        email: this.email,
                        number: this.phoneNumber,
                        address: this.address,
                        transaction_total: this.subtotal,
                        transaction_status: "PENDING",
                        transaction_details: idProduk,
                        transaction_product: this.Cart,
                        bukti_transaksi: this.file,
                    }
                    axios.post('//admin-enerel.delapain.com/api/checkout', data, {
                        headers: {
                            'accept': 'application/json',
                            'Accept-Language': 'en-US,en;q=0.8',
                            'Content-Type': `multipart/form-data`,
                        }
                    })
                        .then((res) => {
                            console.log(res)
                            const data = res.data.meta;
                            if (data.status === 'Success' || data.code === 200) {
                                this.$router.push({ name: 'success' })

                                localStorage.removeItem('cart')
                                localStorage.removeItem('subtotal')
                                localStorage.removeItem('quantityItem')
                            }
                        })
                        .catch(error => {
                            console.log(error)
                            const errorData = error.response.data.errors;
                            var txt = '<ul class="list-item">'

                            Object.values(errorData).forEach(key => {
                                for (let i = 0; i < key.length; i++) {
                                    const element = key[i];
                                    txt += "<li>" + element + "</li>";
                                }
                            })
                            txt += '</ul>';
                            console.log(txt)
                            Swal.fire({
                                title: "Gagal Validasi",
                                icon: "error",
                                html: txt,
                            });
                        }

                        )
                }).catch(error => console.log(error))

            }



        }
    }
}
</script>