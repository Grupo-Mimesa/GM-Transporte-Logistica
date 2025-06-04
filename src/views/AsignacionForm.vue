<template>
  <DefaultLayout>
    <div class="container mt-4">
      <div>
        <h2 class="mb-4 text-primary">
          Asignacionde transporte
        </h2>

        <form
          class="needs-validation"
          @submit.prevent="submitForm"
        >
          <div class="mb-3">
            <label for="transporte" class="form-label fw-semibold">Nombre del Transporte:</label>
            <input type="text" class="form-control" id="transporte" name="transporte" v-model="asignacion.NombreTransporte" required>
          </div>

          <div class="mb-3">
            <label for="chofer" class="form-label fw-semibold">Nombre del Chofer:</label>
            <input type="text" class="form-control" id="chofer" name="chofer" v-model="asignacion.NombreChofer" required>
          </div>

          <div class="mb-3">
            <label for="placa" class="form-label fw-semibold">Placa:</label>
            <input type="text" class="form-control" id="placa" name="placa" v-model="asignacion.Placa" required>
          </div>

          <div class="mb-3">
            <label for="cedula" class="form-label fw-semibold"
              >Cedula de Identidad:</label
            >
            <div class="col-sm-9">
              <input
                type="number"
                class="form-control"
                id="cedula"
                name="cedula"
                v-model="asignacion.Cedula"
                required
              />
            </div>
          </div>

        </form>
      </div>
    </div>
  </DefaultLayout>
</template>

<script>
import DefaultLayout from '@/layouts/DefaultLayout.vue';
import { ref } from "vue";

const asignacion = ref({
  NombreTransporte: '',
  NombreChofer: '',
  Placa: '',
  Cedula: '',
  Fecha: null,
  SKU: '',
  TM: null,
  Cliente: '',
  Pedido: '',
});

const submitForm = async () => {
  const formData = {...asignacion};
  fetch(import.meta.env.VITE_SUBMIT_ASIGNACION_API, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(formData),
  }).then((response) => {
    if (response.ok) {
      alert("Datos enviados correctamente!");
    } else {
      alert("Error al enviar datos.");
    }
  });
}
</script>

<style>

</style>