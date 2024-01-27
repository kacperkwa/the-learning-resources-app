<template>
  <BaseDialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
    <template #default>
      <p>Unfortunately, at least one input value is invalid.</p>
      <p>
        Please check all inputs and make sure you enter at least few characters.
      </p>
    </template>
    <template #actions>
      <BaseButton @click="confirmError">Okay</BaseButton>
    </template>
  </BaseDialog>
  <BaseCard>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="tittle" type="text" ref="titleInput" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea
          ref="descInput"
          name="description"
          id="description"
          rows="3"
        ></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input ref="linkInput" id="link" name="link" type="url" />
      </div>
      <div class="form-control">
        <BaseButton type="submit">Add Resource</BaseButton>
      </div>
    </form>
  </BaseCard>
</template>
<script setup>
import { inject, ref } from 'vue';
const titleInput = ref(null);
const descInput = ref(null);
const linkInput = ref(null);
const addResource = inject('addResource');
const inputIsInvalid = ref(false);

const submitData = () => {
  const enteredTitle = titleInput.value.value;
  const enteredDescription = descInput.value.value;
  const enteredLink = linkInput.value.value;

  if (
    enteredTitle.trim() === '' ||
    enteredDescription.trim() === '' ||
    enteredLink.trim() === ''
  ) {
    inputIsInvalid.value = true;
    return;
  }

  addResource(enteredTitle, enteredDescription, enteredLink);
  titleInput.value.value = '';
  descInput.value.value = '';
  linkInput.value.value = '';
};
const confirmError = () => {
  inputIsInvalid.value = false;
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
