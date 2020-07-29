<template>
  <div>
    <input
      v-model="searchValue"
      class="search-input"
      name="search"
      type="text"
      placeholder="Search galaxies"
      @input="$emit('search', searchValue)"
    >
  </div>
</template>

<script>
export default {
  name: 'SearchInput',
  data () {
    return {
      searchValue: ''
    }
  }
}
</script>

<style>
.search-input {
  padding: 10px 35px;
  width: 270px;
  border: 1px solid #E0E0E0;
  background: url(../assets/icons8-search.svg) no-repeat 11px 11px;
}
</style>
