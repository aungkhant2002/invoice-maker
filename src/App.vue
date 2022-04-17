<template>
    <div class="container">
        <div class="row my-3">
            <div class="col-12">
                <h3 class="text-primary fw-bold text-center">Invoice Maker</h3>
                <form action="" @submit.prevent="saveRecord">
                    <div class="row g-1">
                        <div class="col-6">
                            <select v-model="selectedProduct" id="" class="form-select" required>
                                <option value="0" selected disabled>Select Category</option>
                                <option v-for="product in products" :value="product.id" :key="product.id">{{ product.name }} (${{ product.price }})</option>
                            </select>
                        </div>
                        <div class="col">
                            <input type="number" v-model.number="inputQuantity" placeholder="Quantity" class="form-control" required>
                        </div>
                        <div class="col">
                            <button class="btn btn-primary w-100">
                                <i class="fa-solid fa-plus"></i>
                            </button>
                        </div>
                    </div>
                </form>

                <table class="mt-3 table table-bordered">
                    <thead>
                    <tr>
                        <th>#</th>
                        <th>Name</th>
                        <th>Unit Price</th>
                        <th>Quantity</th>
                        <th>Cost</th>
                    </tr>
                    </thead>
                    <tbody>
                    <tr v-for="(record, index) in records" :key="index">
                        <td>{{ ++index }}</td>
                        <td>{{ record.product.name }}</td>
                        <td>{{ record.product.price }}</td>
                        <td>{{ record.quantity }}</td>
                        <td>{{ record.cost }}</td>
                    </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            products: [
                {id: 1, name: "Apple", price: 50},
                {id: 2, name: "Orange", price: 55},
                {id: 3, name: "Mango", price: 150},
            ],
            selectedProduct: "",
            inputQuantity: "",
            records: [],
        }
    },

    methods: {
        saveRecord() {
            let currentProduct = this.products.find(el => el.id === this.selectedProduct);
            let calcCost = currentProduct.price * this.inputQuantity;
            let record = {
                product: currentProduct,
                quantity: this.inputQuantity,
                cost: calcCost,
            }

            this.records.push(record);
            this.selectedProduct = this.inputQuantity = "";
        }
    },
}
</script>

<style lang="scss">

@import url('https://fonts.googleapis.com/css2?family=Padauk:wght@400;700&family=Poppins:wght@100;200;300;400;500;600;700;800;900&display=swap');

$font-family-sans-serif:  'Padauk', 'Poppins', sans-serif;

@import "~bootstrap/scss/bootstrap";
@import "~@fortawesome/fontawesome-free/css/all.min.css";

</style>