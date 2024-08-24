<template>
    <div>
        <form @submit.prevent="submitForm">
            <div class="mb-3">
                <label for="email" class="form-label">Email:</label>
                <input type="email" class="form-control" v-model="email">
                <span class="text-danger" v-if="errors.email">{{ errors.email[0] }}</span>
            </div>
            <div class="mb-3">
                <label for="password" class="form-label">Password:</label>
                <input type="password" class="form-control" v-model="password">
                <span class="text-danger" v-if="errors.password">{{ errors.password[0] }}</span>
            </div>
            <button type="submit" class="btn btn-primary">Login</button>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            errors: {}
        };
    },
    methods: {
        submitForm() {
            axios.post('/login', {
                email: this.email,
                password: this.password
            }).then(response => {
                window.location.href = '/';
            }).catch(error => {
                if (error.response.status === 422) {
                    this.errors = error.response.data.errors;
                }
            });
        }
    }
}
</script>
