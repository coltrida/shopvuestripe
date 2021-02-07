<template>
    <div class="w-full">
        <div class="lg:w-2/3 w-full mx-auto mt-8 overflow-auto">
            <table class="table-auto w-full text-left whitespace-no-wrap">
                <thead>
                <tr>
                    <th class="px-4 py-3 title-font tracking-widest font-medium text-gray-900 text-sm bg-gray-200 rounded-tl rounded-bl">
                        Item
                    </th>
                    <th class="px-4 py-3 title-font tracking-widest font-medium text-gray-900 text-sm bg-gray-200">
                        Quantity
                    </th>
                    <th class="px-4 py-3 title-font tracking-widest font-medium text-gray-900 text-sm bg-gray-200">
                        Price
                    </th>
                    <th class="px-4 py-3 title-font tracking-widest font-medium text-gray-900 text-sm bg-gray-200">
                        Actions
                    </th>
                </tr>
                </thead>
                <tbody>
                <tr v-for="(item, index) in cart" :key="item.id">
                    <td class="p-4" v-text="item.name"></td>
                    <td class="p-4" v-text="item.quantity"></td>
                    <td class="p-4" v-text="CartLineTotal(item)"></td>
                    <td class="w-10 text-right">
                        <button
                                class="flex ml-auto text-sm text-white bg-indigo-500 border-0 py-2 px-6 focus:outline-none hover:bg-indigo-600 rounded"
                                @click="$store.commit('removeFromCart', index)"
                        >Remove
                        </button>
                    </td>
                </tr>
                <tr>
                    <td class="p-4 font-bold">Total Amount</td>
                    <td class="p-4 font-bold" v-text="cartQuantity"></td>
                    <td class="p-4 font-bold" v-text="cartTotal"></td>
                    <td class="w-10 text-right"></td>
                </tr>
                </tbody>
            </table>
        </div>
        <div class="lg:w-2/3 w-full mx-auto mt-8">
            <div class="flex flex-wrap -mx-2 mt-8">
                <div class="p-2 w-1/3">
                    <div class="relavite">
                        <label for="first_name" class="leading-7 text-sm text-gray-600">First Name</label>
                        <input
                                type="text"
                                id="first_name"
                                name="first_name"
                                class="w-full gr-gray-100 rounded border border-gray-300 focus:border-indigo-500 text-gray700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                                v-model="customer.first_name"
                                :disabled="paymentProcessing"
                        >
                    </div>
                </div>
                <div class="p-2 w-1/3">
                    <div class="relavite">
                        <label for="last_name" class="leading-7 text-sm text-gray-600">Last name</label>
                        <input
                                type="text"
                                id="last_name"
                                name="last_name"
                                class="w-full gr-gray-100 rounded border border-gray-300 focus:border-indigo-500 text-gray700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                                v-model="customer.last_name"
                                :disabled="paymentProcessing"
                        >
                    </div>
                </div>
                <div class="p-2 w-1/3">
                    <div class="relavite">
                        <label for="email" class="leading-7 text-sm text-gray-600">Email</label>
                        <input
                                type="email"
                                id="email"
                                name="email"
                                class="w-full gr-gray-100 rounded border border-gray-300 focus:border-indigo-500 text-gray700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                                v-model="customer.email"
                                :disabled="paymentProcessing"
                        >
                    </div>
                </div>
            </div>
            <div class="flex flex-wrap -mx-2 mt-4">
                <div class="p-2 w-1/3">
                    <div class="relavite">
                        <label for="address" class="leading-7 text-sm text-gray-600">Address</label>
                        <input
                                type="text"
                                id="address"
                                name="address"
                                class="w-full gr-gray-100 rounded border border-gray-300 focus:border-indigo-500 text-gray700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                                v-model="customer.address"
                                :disabled="paymentProcessing"
                        >
                    </div>
                </div>
                <div class="p-2 w-1/3">
                    <div class="relavite">
                        <label for="city" class="leading-7 text-sm text-gray-600">City</label>
                        <input
                                type="text"
                                id="city"
                                name="city"
                                class="w-full gr-gray-100 rounded border border-gray-300 focus:border-indigo-500 text-gray700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                                v-model="customer.city"
                                :disabled="paymentProcessing"
                        >
                    </div>
                </div>
                <div class="p-2 w-1/6">
                    <div class="relavite">
                        <label for="state" class="leading-7 text-sm text-gray-600">State</label>
                        <input
                                type="text"
                                id="state"
                                name="state"
                                class="w-full gr-gray-100 rounded border border-gray-300 focus:border-indigo-500 text-gray700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                                v-model="customer.state"
                                :disabled="paymentProcessing"
                        >
                    </div>
                </div>
                <div class="p-2 w-1/6">
                    <div class="relavite">
                        <label for="zip_code" class="leading-7 text-sm text-gray-600">Zip Code</label>
                        <input
                                type="email"
                                id="zip_code"
                                name="zip_code"
                                class="w-full gr-gray-100 rounded border border-gray-300 focus:border-indigo-500 text-gray700 py-1 px-3 leading-8 transition-colors duration-200 ease-in-out"
                                v-model="customer.zip_code"
                                :disabled="paymentProcessing"
                        >
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Checkout",
        data() {
            return {
                customer: {
                    first_name: '',
                    last_name: '',
                    email: '',
                    address: '',
                    city: '',
                    state: '',
                    zip_code: ''
                },
                paymentProcessing: false
            }
        },
        methods: {
            CartLineTotal(item) {
                let price = (item.price * item.quantity);
                price = (price / 100);
                return price.toLocaleString('it-IT', {style: 'currency', currency: 'EUR'});
            }
        },
        computed: {
            cart() {
                return this.$store.state.cart;
            },
            cartQuantity() {
                return this.$store.state.cart.reduce((acc, item) => acc + item.quantity, 0);
            },
            cartTotal() {
                let price = this.cart.reduce((acc, item) => acc + (item.price * item.quantity), 0);
                price = (price / 100);
                return price.toLocaleString('it-IT', {style: 'currency', currency: 'EUR'});
            }
        }
    }
</script>

<style scoped>

</style>
