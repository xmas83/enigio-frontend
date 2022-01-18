<template>
    <div id="app">
        <Form :addData="addData"/>
        <SearchBar :onsearch="onsearch" :search="search"/>
        <div class="contact-list">
            <ContactItem v-for="(item, index) in displayData" :key="index" :num="index" :data="item"
                         :deleteData="deleteData"/>
        </div>
    </div>
</template>

<script>
  import Form from "./components/Form.vue"
  import SearchBar from "./components/SearchBar.vue"
  import ContactItem from "./components/ContactItem.vue"

  import axios from 'axios';

  import {domain} from './config';

  export default {
    name: "App",
    data() {
      return {
        contact: [],
        search: ""
      }
    },
    components: {
      Form,
      SearchBar,
      ContactItem
    },
    computed: {
      displayData: function () {
        console.log(this.search !== "")
        if (this.search !== "") {
          return this.contact.filter(item => {
            if (item.firstName == this.search) {
              return item;
            }
          })
        } else {
          return this.contact;
        }
      }
    },
    methods: {
      addData: async function (data) {
        await axios.post(domain + '/api/contacts', data);
        this.getData();
      },
      deleteData: async function (id) {
        await axios.delete(domain + '/api/contacts/' + id);
        this.getData();
      },
      getData: async function () {
        let res = await axios.get(domain + '/api/contacts');
        this.contact = res.data;
      },
      onsearch: function (e) {
        this.search = e.target.value;
      }
    },
    async created() {
      let res = await axios.get(domain + '/api/contacts');
      this.contact = res.data;
    }
  }
</script>
<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        width: 60%;
        max-width: 900px;
        min-width: 300px;
        margin: 0 auto;
    }

    .contact-list {
        margin-top: 30px;
        display: grid;
        grid-template-columns: repeat(3, minmax(0, 1fr));
        gap: 10px;
    }

    @media only screen and (max-width: 1000px) {
        .contact-list {
            grid-template-columns: repeat(2, minmax(0, 1fr));
        }
    }

    @media only screen and (max-width: 700px) {
        .contact-list {
            grid-template-columns: repeat(1, minmax(0, 1fr));
        }
    }

    button {
        display: inline-block;
        font-weight: 400;
        text-align: center;
        white-space: nowrap;
        vertical-align: middle;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
        border: 1px solid transparent;
        padding: 6px 16px;
        font-size: 1rem;
        line-height: 1.5;
        border-radius: 0.25rem;
        transition: color .15s ease-in-out, background-color .15s ease-in-out, border-color .15s ease-in-out, box-shadow .15s ease-in-out;
        color: #fff;
        background-color: #dc3545;
        cursor: pointer;
    }

    button:hover {
        color: #fff;
        background-color: #c82333;
        border-color: #bd2130;
    }
</style>
