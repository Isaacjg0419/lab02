<template>
    <div class="mt-5 d-flex justify-content-center">
        <div class="row">
            <div class="col-md-8 offset-md-2">
                <h1 class="text-center">User Information Form</h1>
                <form @submit.prevent="submitForm">
                    <div class="row mb-3">
                        <div class="col-md-6">
                            <label for="username" class="form-label">Username</label>
                            <input type="text" class="form-control" id="username" v-model="formData.username">
                        </div>
                        <div class="col-md-6">
                            <label for="password" class="form-label">Password</label>
                            <input type="password" class="form-control" id="password" v-model="formData.password">
                        </div>
                    </div>
                    <div class="row mb-3">
                        <div class="col-md-6">
                            <div class="form-check">
                                <input type="checkbox" class="form-check-input" id="isAustralian"
                                    v-model="formData.isAustralian">
                                <label for="isAustralian" class="form-check-label">
                                    Australian Resident?
                                </label>
                            </div>
                        </div>
                        <div class="col-md-6">
                            <label for="gender" class="form-label">Gender</label>
                            <select class="form-select" id="gender" v-model="formData.gender">
                                <option value="male">Male</option>
                                <option value="female">Female</option>
                                <option value="other">Other</option>
                            </select>
                        </div>
                    </div>
                    <div class="mb-3">
                        <label for="reason" class="form-label">Reason for joining</label>
                        <textarea class="form-control" id="reason" rows="3" v-model="formData.reason"></textarea>
                    </div>
                    <div class="text-center">
                        <button type="submit" class="btn btn-primary me-2">Submit</button>
                        <button type="button" class="btn btn-secondary" @click="clearForm">Clear</button>
                    </div>
                    <div class="row mt-5" v-if="submittedCards.length">
                        <div class="d-flex flex-wrap justify-content-start">
                            <div v-for="(card, index) in submittedCards" :key="index" class="card">
                                <div class="card-header">
                                    User Information
                                </div>
                                <ul class="list-group list-group-flush">
                                    <li class="list-group-item">Username: {{ card.username }}</li>
                                    <li class="list-group-item">Password: {{ card.password }}</li>
                                    <li class="list-group-item">Australian Resident: {{ card.isAustralian ? 'Yes' : 'No'
                                        }}</li>
                                    <li class="list-group-item">Gender: {{ card.gender }}</li>
                                    <li class="list-group-item">Reason: {{ card.reason }}</li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const formData = ref({
    username: '',
    password: '',
    isAustralian: false,
    reason: '',
    gender: ''
});

const submittedCards = ref([]);

const submitForm = () => {
    submittedCards.value.push({
        ...formData.value
    });
};
const clearForm = () => {
    formData.value = {
        username: '',
        password: '',
        isAustralian: false,
        reason: '',
        gender: ''
    };
};
</script>

<style scoped>
/* Tag selectors */
h1 {
    text-align: center;
    margin-top: 20px;
}

.card {
    border: 1px solid #ccc;
    border-radius: 10px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    margin: 10px;
    flex: 1 1 200px;
}

.card-header {
    background-color: #275FDA;
    color: white;
    padding: 10px;
    border-radius: 10px 10px 0 0;
}

.list-group-item {
    padding: 10px;
}

/* Class selectors */
.form {
    text-align: center;
    margin-top: 50px;
}

/* ID selectors */
#username:focus,
#password:focus,
#isAustralian:focus,
#reason:focus {
    border-color: #FF6347;
    background-color: #FFEBE8;
}

/* Attribute selectors */
select[id="gender"] {
    background-color: #d3d3d3;
}

/* Flexbox styles for card container */
.d-flex {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
}
</style>
