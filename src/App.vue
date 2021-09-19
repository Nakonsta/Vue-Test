<template>
  <div id="app">
    <div class="wrapper">
      <div class="container">
        <div class="col-12">
          <Table
            v-if="users.length"
            :users="users"
          />
          <Modal 
            @saveUser="pushUser"
            :users="users"
          />
          <b-button v-b-modal.adding-modal variant="primary">Добавить</b-button>
        </div>

      </div>
    </div>

  </div>
</template>

<script>
import Table from './components/Table.vue'
import Modal from './components/Modal.vue'
import { BButton, VBModal } from 'bootstrap-vue'

export default {
  name: 'App',
  components: {
    Table,
    Modal,
    BButton
  },
  data: function() {
    return {
      users: [],
    }
  },
  computed: {
    usersCount: function() {
      return this.users.length
    }
  },
  mounted() {
    if(localStorage.getItem('users')) {
      try {
        this.users = JSON.parse(localStorage.getItem('users'));
      } catch(e) {
        localStorage.removeItem('users');
      }
    }
  },
  directives: { 
    'b-modal': VBModal 
  },
  methods: {
    pushUser(name, phone) {
      let newUser = {
        id: this.usersCount,
        name: name,
        phone: phone
      }
      this.users.push(newUser);
      this.saveUser();
    },
    saveUser() {
      const parsedData = JSON.stringify(this.users);
      localStorage.setItem('users', parsedData);
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0,0,0,0);
  white-space: nowrap;
  border: 0;
}
.text-small {
  font-size: 0.8rem;
}
.custom-control-label:before, .custom-file-label, .custom-select {
  transition: background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
}
/* .custom-select {
  display: inline-block;
  width: 100%;
  height: calc(1.5em + .75rem + 2px);
  padding: .375rem 1.75rem .375rem .75rem;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.5;
  color: #495057;
  vertical-align: middle;
  background: #fff;
  border: 1px solid #ced4da;
  border-radius: .25rem;
  appearance: none;
} */
</style>
