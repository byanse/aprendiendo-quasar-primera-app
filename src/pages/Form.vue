<template>
  <q-page padding>
    <h4>Agregar Productos</h4>
    <pre>{{ producto }}-{{ seleccion }}-{{ terminos }}</pre>

    <q-form
      class="row q-col-gutter-md"
      @submit.prevent="procesarFormulario"
      @reset="reset"
      ref="myForm"
    >
      <div class="col-12 col-sm-6">
        <q-input
          label="Producto"
          v-model="producto"
          lazy-rules
          :rules="[
            (val) => (val && val.length > 0) || 'Por favor escribe algo',
          ]"
        />
      </div>

     

      <div class="col-12 col-sm-6">
        <q-select
          label="Proridad"
          v-model="seleccion"
          :options="opciones"
           lazy-rules
          :rules="[
            (val) => (val && val.length > 0) || 'Por favor escribe algo',
          ]"
        />
      </div>

       <div class="col-12">
        <q-toggle label="Aceptar los términos" v-model="terminos" />
      </div>

      <div class="col-12">
        <q-btn label="Submit" color="secondary" type="submit" />
        <q-btn
          label="Reset"
          color="secondary"
          outline
          class="q-ml-sm"
          :ripple="false"
          type="reset"
        />
      </div>
    </q-form>
  </q-page>
</template>

<script>
import { ref } from "vue";
import { useQuasar } from "quasar";

export default {
  setup() {
    const $q = useQuasar();
    const myForm = ref(null);
    const producto = ref(null);
    const seleccion = ref(null);
    const terminos = ref(false);
    const opciones = ["maxima", "moderada", "minima"];

    const procesarFormulario = () => {
      console.log("me diste click al formulario");
      if (terminos.value === false) {
        $q.notify({
          color: "red-5",
          textColor: "white",
          icon: "warning",
          message: "You need to accept the license and terms first",
        })
        myForm.value.resetValidation()
        reset()
      }
      else {
          $q.notify({
            color: 'green-4',
            textColor: 'white',
            icon: 'cloud_done',
            message: 'Submitted'
          })
        }
    };

    const reset = () => {
      producto.value = null;
      seleccion.value = null;
      terminos.value = false;
    };

    return {
      producto,
      seleccion,
      opciones,
      procesarFormulario,
      terminos,
      reset,
      myForm
    };
  },
};
</script>
