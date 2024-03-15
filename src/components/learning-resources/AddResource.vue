<template>
  <base-dialog v-if="inputIsInvalod" title="InvalidInput" @close="confirmError">
  <template #default>
    <p>Unfortunatoly, at least one input is invalid</p>
    <p>Please check all inputs and make sure you enter at least a few characters into each input fields</p>
  </template>
  <template #actions>
    <the-button @click="confirmError">Okay</the-button>
  </template>
</base-dialog>
    <base-card>
    <form @submit.prevent="submitData">
        <div class="form-control">
            <label for="title">Title</label>
            <input type="text" id="title" name="title" ref="titleInput">
        </div>
        <div class="form-control">
            <label for="description">Description</label>
            <textarea id="description" name="description" rows="3" ref="deskInput" ></textarea>
        </div>
        <div class="form-control">
            <label for="link">Link</label>
            <input type="url" id="link" name="link" ref="linkInput">
        </div>
        <div>
            <the-button type="submit">Add Resource</the-button>
        </div>
    </form>
    </base-card>
</template>

<script>
export default {
  data(){
    return {
      inputIsInvalod: false
    }
  },
  inject: ['addRes'],
  methods: {
    submitData(){
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.deskInput.value;
      const enteredLink = this.$refs.linkInput.value;
      if(enteredTitle.trim() === '' || enteredDescription.trim() === '' || enteredLink.trim() === ''){
        this.inputIsInvalod = true;
        return
      } else {
      

      this.addRes(enteredTitle, enteredDescription, enteredLink)
      }
      
    },
    confirmError(){
      this.inputIsInvalod = false;
    }
  }
}
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