<template>
  <div id="app">
    <div class="control-panel">
      <form @submit.prevent="agregarCita">
        <div class="form-group">
          <label for="patient">Paciente</label>
          <input id="patient" type="text" v-model="paciente" required>
        </div>
        <div class="form-group">
          <label for="date">Fecha</label>
          <input id="date" type="date" v-model="fecha" required>
        </div>
        <div class="form-group">
          <label for="hour">Hora</label>
          <input id="hour" type="time" v-model="hora" required>
        </div>
        <div class="form-group">
          <label for="gravity">Gravedad</label>
          <select id="gravity" v-model="gravedad" required>
            <option value="" disabled>--</option>
            <option value="baja">Baja</option>
            <option value="media">Media</option>
            <option value="alta">Alta</option>
          </select>
        </div>
        <div class="form-group">
          <label for="reason">Motivo</label>
          <input id="reason" type="text" v-model="motivo" required>
        </div>
        <div>
          <input type="submit" value="Agregar" :disabled="!paciente || !fecha || !hora || !gravedad || !motivo">
        </div>
      </form>
    </div>
    <p v-if="citas.length === 0" class="no-citas">Aún no hay consultas registradas.</p>
    
    <div v-for="(cita, index) in citas" :key="index">
      <cita-card :cita="cita" @eliminar="eliminarCita"></cita-card>
    </div>
  </div>
</template>

<script>
import CitaCard from './components/CitaCard.vue';

export default {
  name: 'App',
  components: {
    CitaCard
  },
  data() {
    return {
      paciente: '',
      fecha: '',
      hora: '',
      gravedad: '',
      motivo: '',
      citas: []
    };
  },
  methods: {
    agregarCita() {
      this.citas.push({
        paciente: this.paciente,
        fecha: this.fecha,
        hora: this.hora,
        gravedad: this.gravedad,
        motivo: this.motivo
      });
      this.paciente = '';
      this.fecha = '';
      this.hora = '';
      this.gravedad = '';
      this.motivo = '';
    },
    eliminarCita(cita) {
      this.citas = this.citas.filter(item => item !== cita);
    }
  }
};
</script>

<style>
.control-panel {
  padding: 30px;
  border: 1px solid #141313;
  border-radius: 8px;
}

form {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 15px;
}

.form-group {
  display: flex;
  flex-direction: column;
}

label {
  margin-bottom: 5px;
  font-weight: bold;
  color: #f40606;
  text-align: center;
}

input[type="text"], input[type="date"], input[type="time"], select {
  padding: 5px;
  border: 2px solid #ccc;
  border-radius: 4px;
  margin-bottom: 10px;
}

button {
  padding: 10px;
  border-radius: 4px;
  background-color: #4CAF50;
  color: gray;
}

button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

.no-citas {
  margin-top: 20px;
  text-align: center;
  color: #f40606;
}

.empty {
  color: #f40606;
}

.filled {
  color: black;
}
</style>
