<template>
  <v-text-field
    placeholder="Search"
    prepend-inner-icon="mdi-magnify"
    filled
    dense
    clearable
    outlined
    class="expanding-search mt-1"
    :class="{'closed' : searchClosed && !$store.state.search}"
    @focus="searchClosed = false"
    @blur="searchClosed = true"
    :value="$store.state.search"
    @input="$store.commit('setSearch', $event)"
  ></v-text-field>
</template>

<script>
  export default {
    data() {
      return {
        searchClosed: true,
      }
    }
  }
</script>

<style lang="sass">
  .expanding-search
    transition: max-width 0.3s
    .v-input__slot
      cursor: pointer !important
    &.closed
      max-width: 45px
      .v-input__slot
        background: transparent !important
</style>