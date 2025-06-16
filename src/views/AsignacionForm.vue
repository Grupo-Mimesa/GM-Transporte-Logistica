<template>
  <DefaultLayout>
    <section class="container p-4">
      <div class="row justify-content-center">
          <div class="col-md-10">
            <div class="card p-4">
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
                <label for="cedula" class="form-label fw-semibold"
                  >Cedula de Identidad:</label
                >
                <input
                  type="number"
                  class="form-control"
                  id="cedula"
                  name="cedula"
                  v-model="asignacion.Cedula"
                  required
                />
              </div>

              <div class="mb-3">
                <label for="placa" class="form-label fw-semibold">Placa:</label>
                <input type="text" class="form-control" id="placa" name="placa" v-model="asignacion.Placa" required>
              </div>

              <div class="mb-3">
                <label for="fecha" class="form-label fw-semibold">Fecha:</label>
                <input type="date" class="form-control" id="fecha" name="fecha" v-model="asignacion.Fecha" required>
              </div>

              <div class="mb-3">
                <label for="sku" class="form-label fw-semibold">SKU:</label>
                <input type="text" class="form-control" id="sku" name="sku" v-model="asignacion.SKU" required>
              </div>

              <div class="mb-3">
                <label for="tm" class="form-label fw-semibold">TM:</label>
                <input
                  type="number"
                  class="form-control"
                  id="tm"
                  name="tm"
                  v-model="asignacion.TM"
                  required
                />
              </div>

              <div class="mb-3">
                <label for="cliente" class="form-label fw-semibold">Cliente:</label>
                <input type="text" class="form-control" id="cliente" name="cliente" v-model="asignacion.Cliente" required>
              </div>

              <div class="mb-3">
                <label for="pedido" class="form-label fw-semibold">Pedido:</label>
                <input type="text" class="form-control" id="pedido" name="pedido" v-model="asignacion.Pedido" required>
              </div>

              <div class="text-end">
                <button type="submit" class="btn btn-primary ">Guardar</button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </section>
  </DefaultLayout>
</template>

<script setup>
import DefaultLayout from '@/layouts/DefaultLayout.vue';
import { ref } from "vue";

const asignacion = ref({
  NombreTransporte: '',
  NombreChofer: '',
  Cedula: '',
  Placa: '',
  Fecha: null,
  SKU: '',
  TM: null,
  Cliente: '',
  Pedido: '',
});

const submitForm = async () => {
  asignacion.value.Cedula = asignacion.value.Cedula.toString();
  const formData = {...asignacion.value};
  console.log("Datos a enviar:", formData);
  fetch(import.meta.env.VITE_SUBMIT_ASIGNACION_API, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(formData),
  }).then((response) => {
    if (response.ok) {
      alert("Datos enviados correctamente!");
      asignacion.value = {}
    } else {
      alert("Error al enviar datos.");
    }
  });
}
</script>

<style>

</style>