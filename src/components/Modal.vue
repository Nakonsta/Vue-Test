<template>
  <div>
    <b-modal 
      id="adding-modal"
      ref="adding-modal"
      title="Добавление пользователя"
      hide-header-close
      hide-footer
    >
      <form>
        <div class="row">
          <div class="col-3">
            <label
              for="user-name"
            >Имя</label>
          </div>
          <div class="col-9">
            <input
              id="user-name"
              class="form-control"
              v-model="userName"
              placeholder="Введите имя"
            >
          </div>
        </div>
        <div class="row mt-2">
          <div class="col-3">
            <label
              for="user-phone"
            >Телефон</label>
          </div>
          <div class="col-9">
            <input
              id="user-phone"
              class="form-control"
              v-model="userPhone"
              placeholder="Введите телефон"
              v-mask="'+7(999)999-99-99'"
            >
          </div>
        </div>
        <div class="row mt-3">
            <div class="col d-flex justify-content-end">
                <b-button
                  variant="primary"
                  @click="saveUser"
                >Сохранить</b-button>
            </div>
        </div>
      </form>
    </b-modal>
  </div>
</template>

<script>
import { BButton, BModal } from 'bootstrap-vue'

export default {
  name: 'Modal',
  components: {
    BButton,
    BModal
  },
  data: function() {
    return {
      userName: null,
      userPhone: null
    }
  },
  methods: {
    saveUser() {
      this.$emit('saveUser', this.userName, this.userPhone);
      this.$refs['adding-modal'].hide()
    }
  }
}
</script>