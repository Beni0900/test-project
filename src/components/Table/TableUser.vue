<template>
  <div class="tableRow">
    <div class="tableCell" style="width: 4%">
      <input type="checkbox" :checked="isChecked" @click="checkedHandler(user.id)" />
    </div>
    <div class="tableCell userContainer" style="width: 50%">
      <div class="avatar" :style="{ backgroundColor: getColor(userIndex + 1) }">
        {{ user.name.split(' ')[0][0] + '' + user.name.split(' ')[1][0] }}
      </div>
      <div>
        <p class="userName">{{ user.name }}</p>
        <p class="userEmail">{{ user.email }}</p>
      </div>
    </div>
    <div class="tableCell" style="width: 25%">
      <p
        class="permission"
        :style="{ background: user.permission == 'agent' ? 'lightblue' : 'rgb(248, 168, 255)' }"
      >
        {{ user.permission }}
      </p>
    </div>
    <div class="tableCell">
      <div class="actionsContainer">
        <div class="actionButton" @click="editUser">
          <i class="fa-solid fa-pencil"></i>
        </div>
        <div class="actionButton" @click="deleteElement"><i class="fa-solid fa-trash"></i></div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'TableUser',
  props: {
    user: {
      type: Object,
      required: true
    },
    userIndex: {
      type: Number,
      required: true
    },
    checkedUsers: {
      type: Array,
      required: true
    },
    selectedUser: {
      type: [Number, Boolean],
      default: false
    }
  },
  computed: {
    isChecked() {
      return this.checkedUsers.includes(this.user.id)
    }
  },
  methods: {
    checkedHandler(id: number) {
      this.$emit('check', id)
    },
    editUser() {
      this.$emit('edit', this.user)
    },
    deleteElement() {
      this.$emit('showPop', this.user)
    },
    getColor(id: number) {
      if (id === 1 || id === 6) {
        return '#DE40A3'
      } else if (id % 2 === 0) {
        return '#1C40A3'
      } else {
        return '#31F1AC'
      }
    }
  }
})
</script>

<style scoped lang="scss">
input[type='checkbox'] {
  width: 2vh;
  height: 2vh;
  outline: none;
  border: none;
}
.tableRow {
  display: flex;
  margin-bottom: 3vh;
  border-radius: 1vh;
  padding: 1vh;
  height: 8vh;
  &:hover {
    background-color: rgba(209, 209, 209, 0.411);
  }
  .tableCell {
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    &:first-child {
      border-top-left-radius: 1vh;
      border-bottom-left-radius: 1vh;
    }
    &:last-child {
      border-top-right-radius: 1vh;
      border-bottom-right-radius: 1vh;
    }
  }
  .userContainer {
    display: flex;
    align-items: center;
    .avatar {
      width: 5vh;
      height: 5vh;
      border-radius: 50%;
      display: flex;
      justify-content: center;
      align-items: center;
      color: white;
    }
    p {
      margin: 0.5vh 1vh;
    }
    .userName {
      color: black;
    }
    .userEmail {
      color: grey;
    }
  }
  .permission {
    padding: 0.5vh;
    background-color: rgba(228, 163, 174, 0.671);
    width: 9vh;
    margin: 0;
    border-radius: 1vh;
    text-align: center;
    color: purple;
  }
  .actionsContainer {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    margin-left: 5vh;
    gap: 1vh;
    .actionButton {
      display: none;
      justify-content: center;
      align-items: center;
      height: 4vh;
      width: 4vh;
      border: 0.1vh solid rgb(163, 163, 163);
      color: rgb(163, 163, 163);
      border-radius: 1vh;
      &:hover {
        cursor: pointer;
      }
    }
  }
  &:hover .actionsContainer .actionButton {
    display: flex;
  }
}
</style>
