<template>
    <div class="container my-5">
        <div class="row justify-content-center">
            <div class="col-8">
                <router-link 
                    :to="{ name:'transaction.index' }"
                    class="btn btn-secondary btn-sm rounded shadow-sm my-3"
                >
                    Back
                </router-link>
                <div class="card rounded shadow-sm">
                    <div class="card-header">
                        Create Transaction
                    </div>
                    <div class="card-body">
                        <form @submit.prevent="store()">
                            <div class="mb-3">
                                <label for="" class="form-label">Title</label>
                                <input type="text" class="form-control" v-model="transaction.title">
                                <div v-if="validation.title" class="text-danger">
                                    {{ validation.title[0] }}
                                </div>
                            </div>
                            <div class="mb-3">
                                <label for="" class="form-label">Amount</label>
                                <input type="text" class="form-control" v-model="transaction.amount">
                                <div v-if="validation.amount" class="text-danger">
                                    {{ validation.amount[0] }}
                                </div>
                            </div>
                            <div class="mb-3">
                                <label for="" class="form-label">Type</label>
                                <select class="form-control" v-model="transaction.type">
                                    <option value="expense">Expense</option>
                                    <option value="revenue">Revenue</option>
                                </select>
                                <div v-if="validation.type" class="text-danger">
                                    {{ validation.type[0] }}
                                </div>
                            </div>
                            <div class="mb-3">
                                <button class="btn btn-sm btn-primary" type="submit">Submit</button>
                            </div>
                        </form>                        
                    </div>
                </div>
            </div>    
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import {reactive, ref} from 'vue'
import {useRouter} from 'vue-router'

export default {
    setup() {
        let transaction = reactive({
            title: '',
            amount: '',
            type: '',
        });

        let validation = ref([]);

        let router = useRouter();
        
        function store() {
            axios.post(
                'http://127.0.0.1:8000/api/transactions',
                transaction
            )
            .then((result) => {
                router.push({
                    name: 'transaction.index',
                });
            }).catch((err) => {
                validation.value = err.response.data;
            });
        };        

        return {
            transaction,
            store,
            validation,
            router
        }
    }
}
</script>