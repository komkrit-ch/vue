<template>
    <div id="employee-form">
        <form @submit.prevent="handleSubmit">
            <label for="">Employees name</label>
            <input 
                ref="first"
                type="text"
                :class="{'has-error': submmiting && invalidName }"
                v-model="employee.name" 
                @focus="clearStatus"
                @keypress="clearStatus"                
            >
            <label for="">Employee email</label>
            <input 
                v-model="employee.email" 
                :class="{'has-error': submmiting && invalidEmail }"
                type="text"
                @focus="clearStatus"
            >
            <br>
            <p v-if="error && submitting" class="error-message">
                Please fill out all required fields
            </p>
            <p v-if="success" class="success-message">
                Employee successfully added
            </p>
            <button>Add Employee</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'employee-form',
    data() {
        return {
            submitting: false,
            error: false,
            success: false,
            employee: {
                name: '',
                email:''
            }
        }
    },
    methods: {
        handleSubmit() {           
            this.submitting = true;
            this.clearStatus();
            if (this.invalidName || this.invalidEmail) {
                this.error = true;
                return
            }

            this.$emit('add:employee', this.employee)
            this.$refs.first.focus();

            this.employee = {
                name: '',
                email:''
            }
            this.success = true;             
            this.email = false;             
            this.submitting = false;
        },
        
        clearStatus() {
            this.success = false;
            this.error = false;                
        }
    },    
    computed: {
        invalidName() {
            return this.employee.name === ''
        },
        invalidEmail() {
            return this.employee.email === ''
        }
    }

}
</script>

<style scoped>
    form {
        margin-bottom: 2rem;
    }
    input {
        margin-bottom: 2rem;
    }
    [class*='-message'] {
        font-weight : bold;
    }
    .error-message {
        color: red;
    }
    .success-message {
        color: green;
    }
</style>