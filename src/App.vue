<template>
  <form @submit.prevent="handleSubmit">
    <div v-for="block in blocks" :key="block.token">
      <label :for="block.token">{{ block.props.title }}</label>
        <input
          :type="block.type"
          :placeholder="block.props.placeholder"
          v-model="formData[block.token]"
          :required="typeof block.props.required === 'string' ? formData[block.props.required] : block.props.required"
        />
    </div>
    <button type="submit">Submit</button>
  </form>
</template>

<script setup>
import { ref } from 'vue';

const blocks = ref([
  {
    token: 'PERSON_NAME',
    type: 'text',
    props: {
      title: 'Enter your name',
      required: true,
      placeholder: 'e.g John Doe',
    },
  },
  {
    token: 'IS_PERSON_MINOR',
    type: 'checkbox',
    props: {
      title: 'Is the current person a minor',
      default: false,
    },
  },
  {
    token: 'PERSON_DOB',
    type: 'date',
    props: {
      title: 'Enter your DOB',
      placeholder: 'e.g 01/01/2000',
      required:"IS_PERSON_MINOR"
    },
  },
]);

const formData = ref({});
const handleSubmit = () => {
  console.log('Form submitted:', formData.value);
  resetForm();
};

const resetForm = () => {
  formData.value = {};
};
</script>
