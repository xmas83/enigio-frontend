<template>
    <form class="contact-form" v-on:submit="onSubmit">
        <h1>My Phone Book</h1>
        <div class="contact-body">
            <div class="form-wrap">
                <input
                        class="form-input"
                        placeholder="First Name"
                        v-model="firstName"
                        required
                />
            </div>
            <div class="form-wrap">
                <input
                        class="form-input"
                        placeholder="Last Name"
                        v-model="lastName"
                        required
                />
            </div>
            <div class="form-wrap">
                <input
                        class="form-input"
                        placeholder="Phone Number"
                        v-model="phoneNumber"
                        type="text"
                        required
                        onkeypress="return event.charCode >= 48 && event.charCode <= 57"

                />
            </div>
            <div class="form-wrap">
                <input
                        class="form-input"
                        placeholder="Email Address"
                        v-model="email"
                        type="email"
                        required
                />
            </div>
        </div>
        <div class="form-button">
            <button>
                Create
            </button>
        </div>
    </form>
</template>

<script>
  export default {
    name: 'ContactForm',
    data() {
      return {
        firstName: "",
        lastName: "",
        phoneNumber: "",
        email: ""
      }
    },
    props: {
      addData: Function
    },
    methods: {
      onSubmit: function (e) {
        e.preventDefault();
        this.addData({
          firstName: this.firstName,
          lastName: this.lastName,
          phoneNumber: this.phoneNumber,
          email: this.email
        })
      }
    },
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .contact-form {
        margin-bottom: 10px
    }

    .form-input {
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
        margin: 5px 0;
        width: 100%;
    }

    .contact-body {
        display: grid;
        grid-template-columns: repeat(2, minmax(0, 1fr));
        gap: 10px;
    }

    @media only screen and (max-width: 700px) {
        .contact-body {
            grid-template-columns: repeat(1, minmax(0, 1fr));
        }
    }

    .form-wrap {
        display: flex;
        justify-content: end;
    }

    .form-button {
        display: flex;
        justify-content: end;
    }
</style>
