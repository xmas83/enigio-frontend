<template>
    <div class="contact-item">
        <h2 style='margin-bottom: 5px'>{{data.firstName}}</h2>
        <p>{{data.phoneNumber}}</p>
        <p>{{data.email}}</p>
        <div class="btn-wrap">
            <button v-on:click="deleteData(data.id)">
                Remove
            </button>
        </div>
    </div>
</template>
<script>
  export default {
    name: 'ContactItem',
    props: {
      data: Object,
      deleteData: Function,
      num: Number
    },
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .contact-item {
        border: 1px solid #777;
        border-radius: 10px;
        padding: 15px;
    }

    .btn-wrap {
        display: flex;
        justify-content: end;
    }
</style>


