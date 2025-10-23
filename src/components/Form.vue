<template>
  <div class="container mt-3">
    <h3 class="mb-4 text-center">Búsqueda de Personas</h3>

    <div class="row g-3">
      <div class="col-md-6">
        <label class="form-label">Nombre / Apellido</label>
        <input
          v-model.trim="filtroNombre"
          type="text"
          class="form-control"
          placeholder="Ej.: Juan Pérez"
        />
      </div>
      <div class="col-md-6">
        <label class="form-label">DNI</label>
        <input
          v-model.trim="filtroDni"
          type="text"
          class="form-control"
          placeholder="Ej.: 12345678"
          inputmode="numeric"
        />
      </div>
    </div>

    <div v-if="mostrarAdvertencia" class="alert alert-warning mt-3" role="alert">
      Ingresá <strong>al menos 3 caracteres</strong> en cada filtro que estés usando.
    </div>

    <hr />

    <div class="row g-3 row-cols-1 row-cols-sm-2 row-cols-lg-3">
      <div class="col" v-for="p in personasFiltradas" :key="p.dni">
        <div class="card h-100">
          <div class="card-body">
            <h5 class="card-title mb-1">{{ p.nombre }} {{ p.apellido }}</h5>
            <p class="card-text mb-2">DNI: {{ p.dni }}</p>
            <a class="card-link" :href="`mailto:${p.correo}`">{{ p.correo }}</a>
          </div>
        </div>
      </div>

      <div v-if="personasFiltradas.length === 0" class="col-12">
        <div class="alert alert-info text-center m-0">Sin resultados</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BusquedaPersonas',

  data() {
    return {
      filtroNombre: '',
      filtroDni: '',

      personas: [
        { nombre: 'Daniel', apellido: 'Sanchez', correo: 'danielsanchez68@hotmail.com', dni: '20442873' },
        { nombre: 'Juan',   apellido: 'Perez',   correo: 'j@p.gmail.com',               dni: '12345678' },
        { nombre: 'Ana',    apellido: 'Suarez',  correo: 'a@s.gmail.com',               dni: '87654321' },
        { nombre: 'Lucas',  apellido: 'Cohan',   correo: 'lucascohan27@gmail.com',           dni: '47168954' },
      ],
    };
  },

  computed: {
    nombreUsado() {
      return this.filtroNombre.trim() !== '';
    },
    dniUsado() {
      return this.filtroDni.trim() !== '';
    },

    nombreOK() {
      return !this.nombreUsado || this.filtroNombre.trim().length >= 3;
    },
    dniOK() {
      return !this.dniUsado || this.filtroDni.trim().length >= 3;
    },

    mostrarAdvertencia() {
      return (this.nombreUsado && !this.nombreOK) || (this.dniUsado && !this.dniOK);
    },

    personasFiltradas() {
      const nombre = this.filtroNombre.trim();
      const dni = this.filtroDni.trim();

      if (nombre === '' && dni === '') return this.personas;

      return this.personas.filter((p) => {
        const nombreCompleto = `${p.nombre} ${p.apellido}`;

        if (nombre !== '' && dni === '') return nombreCompleto.includes(nombre);
        if (dni !== '' && nombre === '') return String(p.dni).includes(dni);

        return nombreCompleto.includes(nombre) && String(p.dni).includes(dni);
      });
    },
  },
};
</script>

<style scoped>
.card { min-width: 260px; border-radius: 10px; box-shadow: 0 2px 6px rgba(0,0,0,0.08); }
.card-title, .card-text, .card-link { word-break: normal; overflow-wrap: anywhere; }
</style>
