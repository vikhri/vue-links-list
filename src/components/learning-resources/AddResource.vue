<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="confirmError">
    <template #default>
      <p>One of inputs is invalid</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
      <label for="title">Title</label>
      <input id="title" name="title" type="text" ref="titleInput"/>
      <label for="description">Description</label>
      <input id="description" name="description" type="text" ref="descInput"/>
      <label for="link">Link</label>
      <input id="link" name="link" type="url" ref="urlInput"/>
      </div>
      <div>
        <base-button type="submit" @click="submitData">Add</base-button>
      </div>
    </form>
  </base-card>
</template>
<script>
import BaseCard from "../UI/BaseCard.vue";
import BaseButton from "../UI/BaseButton.vue";
import {reactive} from "vue";
import BaseDialog from "../UI/BaseDialog.vue";

export default {
  components: {BaseButton, BaseDialog},
  inject: ['addResource'],
  data() {
    return {
      inputIsInvalid: false
    }
  },
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDesc = this.$refs.descInput.value;
      const enteredUrl = this.$refs.urlInput.value;

      if (enteredTitle.trim() === '' || enteredUrl.trim() === '' || enteredDesc.trim === '' ) {
        this.inputIsInvalid = true;
        return;
      }


      this.addResource(enteredTitle, enteredDesc, enteredUrl)
    },
    confirmError() {
      this.inputIsInvalid = false;
    }
  }
}

</script>

<style scope>
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