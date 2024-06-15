<template>
  <div class="tableRowCustom" style="margin-top: -2vh">
    <div class="tableCellCustom" style="width: 23%">
      <label for="name">Name</label>
      <input
        type="text"
        id="name"
        placeholder="Enter Name"
        :value="user.name"
        @input="
          (event) => {
            const inputElement = event.target as HTMLInputElement
            newUserData.name = inputElement.value
          }
        "
      />
    </div>
    <div class="tableCellCustom" style="width: 23%">
      <label for="email">Email</label>
      <input
        type="text"
        id="email"
        placeholder="Enter Email"
        :value="user.email"
        @input="
          (event) => {
            const inputElement = event.target as HTMLInputElement
            newUserData.email = inputElement.value
          }
        "
      />
    </div>
    <div class="tableCellCustom" v-if="newUser" style="width: 23%">
      <label for="permission">Permission</label>
      <select
        id="permission"
        :value="user.permission"
        @change="
          (event) => {
            const inputElement = event.target as HTMLSelectElement
            newUserData.permission = inputElement.value
          }
        "
      >
        <option value="agent">Agent</option>
        <option value="admin">Admin</option>
      </select>
    </div>
    <div class="tableCellCustom" v-if="!newUser" style="width: 23%">
      <label for="permission">Permission</label>
      <input
        style="opacity: 0.5"
        type="text"
        id="permission"
        :value="user.permission"
        @input="
          (event) => {
            const inputElement = event.target as HTMLInputElement
            newUserData.email = inputElement.value
          }
        "
        readOnly
      />
    </div>
    <div class="tableCellCustom actionsContainerCustom">
      <button class="actionButton addButton" @click="save()">{{ newUser ? 'Add' : 'Save' }}</button>
      <button class="actionButton cancelButton" @click="hide()">Cancel</button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'TableUserEdit',
  props: {
    user: {
      type: Object,
      required: true
    },
    newUser: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      newUserData: {
        name: this.user.name,
        email: this.user.email,
        permission: this.user.permission
      }
    }
  },
  methods: {
    save() {
      this.$emit('save', this.newUserData)
    },
    hide() {
      this.$emit('cancel', this.newUserData)
    }
  }
})
</script>

<style scoped lang="scss">
.tableRowCustom {
  display: flex;
  align-items: center;
  background-color: #F7FAFC;
  padding: 25px 25px;
  border-radius: 8px;

  .tableCellCustom {
    display: flex;
    flex-direction: column;
    margin-right: 1vh;

    label {
      margin-bottom: 1vh;
      color: #6c757d;
    }

    input,
    select {
      padding: 1vh;
      border: 1px solid #ced4da;
      border-radius: 0.5vh;
      background-color: #f1f3f5;
      outline: none;
      height: 4.3vh;
    }

    input::placeholder {
      color: #adb5bd;
    }

    select {
      color: #868686;
      font-weight: 550;
    }

    select {
      cursor: pointer;
    }
  }
  .actionsContainerCustom {
    display: flex;
    gap: 1vh;
    flex-direction: row;
    margin-left: 2.5vh;
    .actionButton {
      border: none;
      border-radius: 0.5vh;
      cursor: pointer;
      color: #fff;
      height: 4.3vh;
      width: 8vh;
      margin-top: 2.8vh;
      font-size: 1.8vh;

      &.addButton {
        background-color: #4fc3f7;
      }

      &.cancelButton {
        background-color: #d6d6d6;
        color: rgb(100, 100, 100);
      }

      &:hover {
        opacity: 0.8;
      }
    }
  }
}
</style>
