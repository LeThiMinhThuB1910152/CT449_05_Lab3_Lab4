<template>
    <div v-if="contact" class="page">
      <h4>Thêm mới liên hệ</h4>
      <ContactForm :contact="contact" @submit:contact="addContact" />
      <p>{{ message }}</p>
    </div>
  </template>
  
  <script>
  import ContactForm from "@/components/ContactForm.vue";
  import ContactService from "@/services/contact.service";
  
  export default {
    components: {
      ContactForm,
    },
    props: {},
    data() {
      return {
        contact: {},
        message: "",
      };
    },
    methods: {
      async addContact(data) {
        try {
          await ContactService.create(data);
          this.message = "Thêm người dùng thành công!";
          this.$router.push({ name: "ContactBook" });
        } catch (error) {
          console.log(error);
        }
      },
    },
    created() {
      this.message = "";
    },
  };
  </script>