<template>
  <div class="row">
    <div class="col-12">
      <b-table
        :items="users"
        :fields="fields"
        sort-icon-left
        striped
      ></b-table>
    </div>
  </div>
</template>

<script>
import { BTable } from 'bootstrap-vue'

export default {
  name: 'Table',

  props: {
    users: {
      type: Array,
      required: true
    }
  },

  components: {
    BTable
  },

  data() {
    return {
      fields: [
        {
          key: 'name',
          label: 'Имя',
          sortable: true
        },
        {
          key: 'phone',
          label: 'Телефон',
          sortable: true
        },
      ],
    }
  }
}
</script>
