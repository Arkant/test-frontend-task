<template>
  <div class="page-container">
    <div class="page-container-header">
      <h1>Named galaxies</h1>
      <SearchInput @search="(e) => searchValue = e" />
    </div>
    <ItemTable v-if="showTable" :columns="columns" :rows="rows" :search="searchValue" @sort="sort" />
  </div>
</template>

<script>
import axios from 'axios'
import SearchInput from '../components/SearchInput'
import ItemTable from '../components/ItemTable'

export default {
  components: {
    SearchInput,
    ItemTable
  },
  data () {
    return {
      columns: [
        {
          title: 'Galaxy Name',
          origin: 'name'
        },
        {
          title: 'Constelation',
          origin: 'constellation'
        },
        {
          title: 'Origin Of Name',
          origin: 'originOfName'
        }
      ],
      rows: [],
      searchValue: ''
    }
  },
  computed: {
    showTable () {
      return this.rows && this.rows.length > 0
    }
  },
  mounted () {
    this.getData()
  },
  methods: {
    async getData () {
      try {
        const result = await axios.get('/galaxies', {
          headers: {
            'Content-Type': 'application/json'
          }
        })
        this.rows = result.data
      } catch (e) {
        this.error = e.response.statusText
      }
    },
    sort (sortDirection) {
      // лучше было бы сделать сортировку на бэке
      if (sortDirection === 'asc') {
        this.rows = this.rows.sort((a, b) => {
          if (a.name < b.name) { return -1 }
          if (a.name > b.name) { return 1 }
          return 0
        })
      } else {
        this.rows = this.rows.sort((a, b) => {
          if (a.name > b.name) { return -1 }
          if (a.name < b.name) { return 1 }
          return 0
        })
      }
    }
  }
}
</script>

<style lang="scss">
.page-container {
  padding: 70px 60px;

  &-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 60px;
    h1 {
      margin: 0;
    }
  }
}
</style>
