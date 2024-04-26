<template>
  <dialog :open="showForm">
    <h2 class="form-header">Add New Sweet</h2>
    <form>
      <table>
        <tr>
          <td>Id:</td>
          <td><input style="width:50px" v-model="sweetItem.id"></td>
        </tr>
        <tr>
          <td>Type:</td>
          <td><input style="width:200px" v-model="sweetItem.type"></td>
        </tr>
        <tr>
          <td>Name:</td>
          <td><input style="width:200px" v-model="sweetItem.name"></td>
        </tr>
        <tr>
          <td>Topping:</td>
          <td><input style="width:300px" v-model="sweetItem.topping"></td>
        </tr>
      </table>
    </form>
    <div class="form-footer">
      <div v-if="errorMessage" class="error">{{errorMessage}}</div>
      <button class="button cancel" value="cancel" @click="closeForm">Cancel</button>
      <button class="button confirm" @click="addSweet">Confirm</button>
    </div>
  </dialog>
</template>

<script>
export default {
  name: 'SweetFormComponent',
  props: {
    label: null,
    showForm: {
      type: Boolean,
      default: false
    }
  },
  data: () => ({
    sweetItem: {
      id: null,
      type: null,
      name: null,
      topping: null},
    errorMessage: null
  }),
  methods: {
    closeForm() {
      this.$emit("cancel");
    },
    addSweet() {
      if (!this.sweetItem.id && !this.sweetItem.type && !this.sweetItem.name && !this.sweetItem.topping) {
        this.errorMessage = "You must enter at least 1 value.";
        return;
      }

      this.$emit("add", this.sweetItem);
    }
  },
  watch: {
    showForm(newVal) {
      if (newVal) {
        // Reset the form
        this.errorMessage = null;
        this.sweetItem = {
          id: null,
          type: null,
          name: null,
          topping: null
        };
      }
    }
  }
}
</script>

<style scoped>
.form-header {
  margin-top: 0px;
}
.form-footer {
  margin-top: 10px;
  display:grid;
}
.button {
  margin-top: 5px;
}
.button.cancel {
  color: white;
  background: red;
}
.button.confirm {
  color: white;
  background: rgb(7, 165, 7);
}
dialog{
  margin-top: -60px;
  border-radius: 5px;
}
.error {
  color: red;
}
</style>
