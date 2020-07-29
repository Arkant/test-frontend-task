<template>
  <div>
    <table class="table">
      <tr class="table-header">
        <th v-for="(column, index) in columns" :key="index" class="table-header-content">
          <div v-if="column.origin === 'name'" class="table-header-content-sort" @click="onSort">
            <p>
              {{ column.title.toUpperCase() }}
            </p>
            <p v-if="sortDirection === 'asc'">
              &#8593;
            </p>
            <p v-if="sortDirection === 'desc'">
              &#8595;
            </p>
          </div>
          <p v-else class="table-header-content-par">
            {{ column.title.toUpperCase() }}
          </p>
        </th>
      </tr>
      <tr v-for="(row, index) in searchedRows" :key="index" class="table-row">
        <td v-for="(data, key) in row" :key="key" class="table-row-сontainer">
          <div v-if="key === 'name'" class="table-row-сontainer-content">
            <img :src="rows[index]['img']">
            {{ data }}
          </div>
          <div v-if="key === 'constellation'" class="table-row-сontainer-content">
            {{ data }}
          </div>
          <div v-if="key === 'originOfName'" class="table-row-сontainer-content">
            {{ data }}
          </div>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: 'ItemTable',
  props: {
    columns: {
      type: Array,
      default: () => [],
      required: true
    },
    rows: {
      type: Array,
      default: () => [],
      required: true
    },
    search: {
      type: String,
      default: ''
    }
  },
  data () {
    return {
      sortDirection: 'asc'
    }
  },
  computed: {
    requiredRows () {
      return this.rows.map((row) => {
        const newObject = {}
        for (let i = 0; i < this.columns.length; i++) {
          const { origin } = this.columns[i]
          newObject[origin] = row[origin]
        }
        return newObject
      })
    },
    searchedRows () {
      return this.requiredRows.map((el) => {
        if (el.name.toLowerCase().includes(this.search.toLowerCase())) {
          return el
        }
      })
    }
  },
  methods: {
    onSort () {
      if (this.sortDirection === 'asc') {
        this.sortDirection = 'desc'
      } else {
        this.sortDirection = 'asc'
      }
      this.$emit('sort', this.sortDirection)
    }
  }
}
</script>

<style lang="scss" scoped>
.table {
  border-collapse: collapse;

  &-header {
    &-content {
      &-sort {
        display: flex;

        p {
          margin-right: 10px;
          font-size: 14px;
        }
      }
      &-par {
        float: left;
        font-size: 12px;
        font-weight: lighter;
        color: #909597
      }
    }
  }

  &-row {
    &:hover {
      background-color: #dfe6fc;
    }
    &-сontainer{
      text-align: left;
      border: 1px solid #E0E0E0;

      &-content {
        display: flex;
        align-items: center;
        padding: 35px 20px;
        img {
          width: 30px;
          height: 30px;
          margin-right: 20px;
        }
      }
    }
  }

}
</style>
