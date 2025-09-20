<template>
    <div class="container mt-5">

        <form @submit.prevent="evaluateScore" class="mt-3">
            <div class="mb-3">
                <label for="score1" class="form-label">Nota 1</label>
                <input
                    type="number"
                    id="score1"
                    v-model.number="note1"
                    class="form-control"
                    required
                    min="10"
                    max="70"
                >
            </div>
            <div class="mb-3">
                <label for="score2" class="form-label">Nota 2</label>
                <input
                    type="number"
                    id="score2"
                    v-model.number="note2"
                    class="form-control"
                    required
                    min="10"
                    max="70"
                >
            </div>
            <div class="mb-3">
                <label for="score3" class="form-label">Nota 3</label>
                <input
                    type="number"
                    id="score3"
                    v-model.number="note3"
                    class="form-control"
                    required
                    min="10"
                    max="70"
                >
            </div>
            <div class="mb-3">
                <label for="attendance" class="form-label">Asistencia %</label>
                <input
                    type="number"
                    id="attendance"
                    v-model.number="attendance"
                    class="form-control"
                    required
                    min="0"
                    max="100"
                >
            </div>
            <button type="submit" class="btn btn-primary">Evaluar</button>
        </form>

        <div v-if="message" :class="alertClass" class="mt-3" role="alert">
            {{ message }}
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            note1: null,
            note2: null,
            note3: null,
            attendance: null,
            average: null,
            message: '',
            status: ''
        };
    },
    computed: {
        alertClass() {
            if (!this.status) {
                return '';
            }

            return this.status === 'success' ? 'alert alert-success' : 'alert alert-danger';
        }
    },
    methods: {
        evaluateScore() {
            this.message = '';
            this.status = '';
            this.average = null;

            const notes = [this.note1, this.note2, this.note3];

            const promedio = this.note1 * 0.35 + this.note2 * 0.35 + this.note3 * 0.3;
            this.average = Number(promedio.toFixed(2));

            const cumpleprom = this.average >= 40;
            const cumpleasist = this.attendance >= 80;

            if (cumpleprom && cumpleasist) {
                this.status = 'success';
                this.message = `Tu promedio es: ${this.average}.\nTu estado es: Aprobado.`;
            } else {
                this.status = 'error';
                this.message = `Tu promedio es: ${this.average}.\nTu estado es: Reprobado.`;
            }
        }
    }
};
</script>

<style scoped>
    .container {
        max-width: 500px;
        margin: 0 auto;
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
    }

    form {
        width: 100%;
    }

    .mb-3 {
        width: 100%;
    }

    .form-label {
        font-weight: bold;
        text-align: left;
        width: 100%;
    }

    .btn-primary {
        margin: 10px auto 0;
        display: block;
    }

    .alert {
        white-space: pre-line;
        width: 100%;
    }
</style>
