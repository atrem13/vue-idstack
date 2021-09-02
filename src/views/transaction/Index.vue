<template>
    <div class="container my-5">
        <div class="row justify-content-center">
            <div class="col-8">
                <router-link 
                    :to="{ name:'transaction.create' }"
                    class="btn btn-primary btn-sm rounded shadow-sm my-3"
                >
                    Add New Transaction
                </router-link>
                <div class="card rounded shadow-sm">
                    <div class="card-header">
                        Transaction List
                    </div>
                    <div class="card-body">
                        <table class="table">
                            <thead>
                                <tr>
                                    <th>Title</th>
                                    <th>Amount</th>
                                    <th>Type</th>
                                    <th>Action</th>
                                </tr>  
                            </thead>
                            <tbody>
                                <tr v-for="(transaction, index) in transactions" :key="index">
                                    <td>{{ transaction.title }}</td>
                                    <td>{{ transaction.amount }}</td>
                                    <td>{{ transaction.type }}</td>
                                    <td>
                                        <div class="btn-group">
                                            <router-link 
                                                :to="{name: 'transaction.edit', params: {id: transaction.id}}"
                                                class="btn btn-sm btn-outline-primary mr-2" 
                                            >
                                                Edit
                                            </router-link>
                                        </div>  
                                        <div class="btn-group">
                                            <router-link 
                                                :to="{name: 'transaction.edit', params: {id: transaction.id}}"
                                                class="btn btn-sm btn-outline-primary mr-2" 
                                            >
                                                Delete
                                            </router-link>
                                        </div>   
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>    
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import {onMounted, ref} from 'vue'

export default {
    setup() {
        let transactions = ref([]);
        
        onMounted(() => {
            axios.get('http://127.0.0.1:8000/api/transactions')
            .then((result) => {
                transactions.value = result.data.data;
                console.log(transactions.value);
            }).catch((err) => {
                console.log(err.response);
            });
        });

        function DeleteData() {

        };        

        return {
            transactions,
            onMounted
        }
    }
}
</script>