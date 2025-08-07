<template>
  <div class="container">
    <div class="row">
      <div class="col-md-8 offset-md-2">
        <DynamicForm :schema="formSchema" :initialValues="formData" :errors="errors" @submit="getFormValues" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import DynamicForm from './components/DynamicForm.vue';

const errors = {
  "nombres": [
      "El campo nombre ya ha sido registrado."
  ],
  "apellidos": [
      "El campo apellidos ya ha sido registrado."
  ],
};

const formData = ref({
  nombres: 'Juan Pérez',
  apellidos: 'Juan Pérez',
  email: 'juan@ejemplo.com',
  password: '12345678',
  "password-confirm": '12345678',
  pais: 'Guatemala',
  departamento: 7
});

const formSchema = {
  title: 'Registro de usuario',
  submitText: 'Registrar usuario',
  fields: [
    {
      label: 'Nombres',
      name: 'nombres',
      as: 'input',
      rules: 'required|min:10',
      col: 6
    },
    {
      label: 'Apellidos',
      name: 'apellidos',
      as: 'input',
      rules: 'required',
      col: 6
    },
    {
      label: 'Your Email',
      name: 'email',
      as: 'input',
      rules: 'required',
      col: 6
    },
    {
      label: 'Your Password',
      name: 'password',
      as: 'input',
      type: 'password',
      rules: 'required',
      title: 'escriba su passowrd',
      col: 6
    },
    {
      label: 'Confirmar Contraseña',
      name: 'password-confirm',
      as: 'input',
      type: 'password',
      rules: 'required|confirmed:@password',
      title: 'escriba su passowrd',
      col: 6
    },
    {
      label: 'País',
      name: 'pais',
      as: 'select',
      rules: 'required',
      col: 6,
      options: [ // o optionsUrl: 'https://api.com/paises'
        { id: 'GT', name: 'Guatemala'},
        { id: 'MX', name: 'México'},
        { id: 'AR', name: 'Argentina'},
      ],
    },
    {
      label: 'Departamento',
      name: 'departamento',
      as: 'select',
      rules: 'required',
      col: 6,
      optionsUrl: 'https://api-colombia.com/api/v1/Department'
    },
  ],
  sections: [
    {
      title: 'Datos Personales',
      fields: [
        { label: 'Dpi', name: 'dpi', as: 'input', rules: 'required', col: 6 },
        { label: 'Nit', name: 'nit', as: 'input', rules: 'required', col: 6 },
      ],
    },
    {
      title: 'Domicilio',
      fields: [
        { label: 'Dirección', name: 'direccion', as: 'input', rules: 'required', col: 6 },
        { label: 'Zona', name: 'zona', as: 'input', rules: 'required|size:10', col: 6 },
      ],
    },
  ]
};

const getFormValues = (values: Object) => {
  console.log(values);
}
</script>
