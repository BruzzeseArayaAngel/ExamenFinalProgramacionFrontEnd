<template>
    <br><br>
    <form @submit.prevent="submitForm" class="container">
        <div class="form-group">
            <label for="name">Nombre:</label>
            <input
                type="text"
                id="name"
                v-model="form.name"
                @input="validateName"
                class="form-control"
            />
            <p v-if="errors.name" class="error-message">{{ errors.name }}</p>
        </div>
        <div class="form-group">
            <label for="email">Correo:</label>
            <input
                type="email"
                id="email"
                v-model="form.email"
                @input="validateEmail"
                class="form-control"
            />
            <p v-if="errors.email" class="error-message">{{ errors.email }}</p>
        </div>
        <div class="form-group">
            <label for="password">Contraseña:</label>
            <input
                type="password"
                id="password"
                v-model="form.password"
                @input="validatePassword"
                class="form-control"
            />
            <p v-if="errors.password" class="error-message">{{ errors.password }}</p>
        </div>
        <div class="form-group">
            <label for="repeatPassword">Repetir contraseña:</label>
            <input
                type="password"
                id="repeatPassword"
                v-model="form.repeatPassword"
                @input="validateRepeatPassword"
                class="form-control"
            />
            <p v-if="errors.repeatPassword" class="error-message">{{ errors.repeatPassword }}</p>
        </div>
        <div class="form-actions">
            <button type="submit" class="btn btn-primary">Enviar</button>
        </div>
    </form>
</template>

<script>
export default {
    data() {
        return {
            form: {
                name: '',
                password: '',
                repeatPassword: '',
                email: ''
            },
            errors: {
                name: '',
                password: '',
                repeatPassword: '',
                email: ''
            }
        };
    },
    methods: {
        validateName() {
            if (!this.form.name) {
                this.errors.name = 'El campo nombre es requerido';
            } else if (/\d/.test(this.form.name)) {
                this.errors.name = 'El nombre no debe contener números';
            } else {
                this.errors.name = '';
            }
        },
        validatePassword() {
            if (!this.form.password) {
                this.errors.password = 'El campo contraseña es requerido';
            } else if (this.form.password.length < 5) {
                this.errors.password = 'La contraseña debe tener al menos 5 caracteres';
            } else {
                this.errors.password = '';
            }

            if (this.form.repeatPassword) {
                this.validateRepeatPassword();
            }
        },
        validateRepeatPassword() {
            if (!this.form.repeatPassword) {
                this.errors.repeatPassword = 'El campo repetir contraseña es requerido';
            } else if (this.form.repeatPassword !== this.form.password) {
                this.errors.repeatPassword = 'Las contraseñas no coinciden';
            } else {
                this.errors.repeatPassword = '';
            }
        },
        validateEmail() {
            if (!this.form.email) {
                this.errors.email = 'El campo correo es requerido';
            } else if (!/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(this.form.email)) {
                this.errors.email = 'El correo es inválido';
            } else {
                this.errors.email = '';
            }
        },
        submitForm() {
            this.validateName();
            this.validatePassword();
            this.validateRepeatPassword();
            this.validateEmail();

            const hasErrors = Object.values(this.errors).some((error) => error !== '');

            if (!hasErrors) {
                alert('El registro se ha realizado correctamente');
            }
        }
    }
};
</script>

<style scoped>
    .container {
        max-width: 520px;
        margin: 60px auto;
        padding: 40px 48px;
        background-color: #ffffff;
        border: 1px solid #e3e6eb;
        border-radius: 12px;
        box-shadow: 0 10px 30px rgba(0, 0, 0, 0.05);
    }

    .form-group {
        width: 100%;
        margin-bottom: 28px;
        text-align: center;
    }

    label {
        display: block;
        margin-bottom: 10px;
        font-weight: 600;
        color: #4a5568;
    }

    .form-control {
        width: 100%;
        padding: 12px 16px;
        border: 1px solid #cbd5e0;
        border-radius: 8px;
        font-size: 16px;
        transition: border-color 0.2s ease, box-shadow 0.2s ease;
    }

    .form-control:focus {
        outline: none;
        border-color: #63b3ed;
        box-shadow: 0 0 0 3px rgba(99, 179, 237, 0.35);
    }

    .error-message {
        margin-top: 6px;
        color: #e53e3e;
        font-size: 14px;
    }

    .form-actions {
        width: 100%;
        display: flex;
        justify-content: flex-start;
        align-self: stretch;
    }

    .btn-primary {
        background-color: #24a15f;
        color: #fff;
        padding: 10px 28px;
        border: none;
        border-radius: 8px;
        font-size: 16px;
        font-weight: 600;
        cursor: pointer;
        transition: background-color 0.2s ease;
    }

    .btn-primary:hover {
        background-color: #059d51;
    }

    .btn-primary:focus {
        outline: none;
        box-shadow: 0 0 0 3px rgba(72, 187, 120, 0.35);
    }

    form {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    button {
        margin-top: 10px;
    }
</style>
