<template>
    <div class="cita-card" :style="{ backgroundColor: getColor() }">
        <p><strong>Paciente:</strong> {{ cita.paciente }}</p>
        <p><strong>Fecha:</strong> {{ cita.fecha }}</p>
        <p><strong>Hora:</strong> {{ cita.hora }}</p>
        <p><strong>Gravedad:</strong> {{ gravedadCompleta }}</p>
        <p><strong>Motivo:</strong> {{ cita.motivo }}</p>
        <button @click="eliminarCita">Eliminar</button>
    </div>
</template>

<script>
export default {
    props: {
        cita: Object
    },
    computed: {
        gravedadCompleta() {
            switch (this.cita.gravedad) {
                case 'baja':
                    return 'Baja';
                case 'media':
                    return 'Media';
                case 'alta':
                    return 'Alta';
                default:
                    return 'Desconocida';
            }
        }
    },
    methods: {
        getColor() {
            switch (this.cita.gravedad) {
                case 'baja':
                    return 'lightgreen';
                case 'media':
                    return 'yellow';
                case 'alta':
                    return 'salmon';
                default:
                    return 'white';
            }
        },
        eliminarCita() {
            this.$emit('eliminar', this.cita);
        }
    }
};
</script>

<style scoped>
.cita-card {
    width: 20%;
    border: 1px solid #000;
    padding: 10px;
    margin-bottom: 10px;
    margin-top: 10px;
    border-radius: 8px;
}

button {
    padding: 5px 10px;
    border: none;
    border-radius: 4px;
    background-color: #696666;
    color: #000;
    cursor: pointer;
    margin-left: 125px;
}

button:hover {
    background-color: #482ab6;
}
</style>