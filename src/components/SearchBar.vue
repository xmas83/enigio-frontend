<template>
    <div class="searchbar">
        <input
                class="input"
                placeholder='search...'
                v-bind:value="search"
                v-on:change="onsearch"
        />
    </div>
</template>
<script>
  export default {
    name: 'SearchBar',
    props: {
      onsearch: Function,
      search: String
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .searchbar {
        display: flex;
        justify-content: end;
    }

    @media only screen and (max-width: 700px) {
        .searchbar input {
            width: 100%;
        }
    }

    .input {
        display: block;
        padding: 0.375rem 0.75rem;
        font-size: 1rem;
        line-height: 1.5;
        color: #495057;
        background-color: #fff;
        background-clip: padding-box;
        border: 1px solid #ced4da;
        border-radius: 0.25rem;
        transition: border-color .15s ease-in-out, box-shadow .15s ease-in-out;
    }
</style>
