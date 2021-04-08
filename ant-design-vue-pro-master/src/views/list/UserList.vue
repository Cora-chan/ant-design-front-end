<template>
  <a-table :columns="columns" :data-source="users">
    <a slot="user" slot-scope="text">{{ text }}</a>
  </a-table>
</template>
<script>
import axios from 'axios'
const columns = [
  {
    title: 'Login',
    dataIndex: 'login',
    key: 'login',
    scopedSlots: { customRender: 'login' }
  },
  {
    title: 'Country',
    dataIndex: 'country',
    key: 'country',
    width: 120
  },
  {
    title: 'Name',
    dataIndex: 'name',
    key: 'name',
    ellipsis: true
  },
  {
    title: 'Group',
    dataIndex: 'group',
    key: 'group',
    ellipsis: true
  },
  {
    title: 'Leverage',
    dataIndex: 'leverage',
    ellipsis: true
  },
  {
    title: 'Balance',
    dataIndex: 'balance',
    key: 'balance',
    ellipsis: true
  }
]

export default {
  data () {
    return {
      users: [],
      errors: [],
      columns
    }
  },
  created () {
      axios.get('http://192.168.0.181:49725/v1/api/users')
      .then(response => {
          this.users = response.data
      })
      .catch(e => {
          this.errors.push(e)
      })
  }
}
</script>
