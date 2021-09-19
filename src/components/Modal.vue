<template>
  <div>
    <b-modal 
      id="adding-modal"
      ref="adding-modal"
      title="Добавление пользователя"
      hide-header-close
      hide-footer
      size="lg"
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
              required
              @input="validateName"
            >
            <div id="user-name-error" class="pt-1 pl-1 d-none text-danger text-small">
              Введите имя
            </div>
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
              type="text"
              class="form-control"
              v-model="userPhone"
              placeholder="Введите телефон"
              v-mask="{
                mask: '+7(999)999-99-99',
              }"
              required
              @input="validatePhoneNumber"
            >
            <div id="user-phone-error" class="pt-1 pl-1 d-none text-danger text-small">
              Введите номер телефона в формате +7(123)456-78-90
            </div>
          </div>
        </div>
        <div class="row mt-2">
          <div class="col-3">
            Начальник
          </div>
          <div class="col-9">
            <b-form-select
              v-model="userParent"
              :options="users"
              class="mb-3 form-select"
              value-field="id"
              text-field="name"
            ></b-form-select>
          </div>
        </div>
        <div class="row mt-3">
            <div class="col d-flex justify-content-end">
                <b-button
                  variant="secondary"
                  @click="closeModal"
                  class="mx-1"
                >Отменить</b-button>
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
import { BButton, BModal, BFormSelect } from 'bootstrap-vue'

export default {
  name: 'Modal',
  components: {
    BButton,
    BModal,
    BFormSelect
  },
  props: {
    users: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      userName: null,
      userPhone: null,
      userParent: null,
      isNameValid: false,
      isPhoneValid: false,
    }
  },
  methods: {
    saveUser() {
      if (!this.isNameValid || !this.isPhoneValid) {
        if (!this.isNameValid) {
          document.querySelector('#user-name-error').classList.remove('d-none');
          }
        if (!this.isPhoneValid) {
          document.querySelector('#user-phone-error').classList.remove('d-none');
        }
        return false;
      }
      this.$emit('saveUser', this.userName, this.userPhone);
      this.closeModal();
    },
    closeModal() {
      this.userName = null;
      this.userPhone = null;
      this.$refs['adding-modal'].hide();
    },
    validatePhoneNumber() {
      const regexPhoneNumber = /^(\+7|7|8)?[\s\-]?\(?[0-9]{3}\)?[\s\-]?[0-9]{3}[\s\-]?[0-9]{2}[\s\-]?[0-9]{2}$/;
	  if (this.userPhone.match(regexPhoneNumber)) {
		this.isPhoneValid = true;
        document.querySelector('#user-phone-error').classList.add('d-none');
	  } else {
        this.isPhoneValid = false;
	  }
    },
    validateName() {
      if(!this.userName) {
        this.isNameValid = false;
      } else {
        document.querySelector('#user-name-error').classList.add('d-none');
        this.isNameValid = true;
      }
    }
  }
}
</script>