<template>
  <div class="page">
    <h4>Thêm liên hệ mới</h4>
    <ContactForm :contact="NewContact" @submit:contact="createContact" />
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
  data() {
    return {
      NewContact: {
        name: "",
        email: "",
        address: "",
        phone: "",
        favorite: false,
      },
      message: "",
    };
  },
  methods: {
    async createContact(data) {
      try {
        await ContactService.create(data);
        alert("Liên hệ mới đã được thêm thành công!");
        this.$router.push({ name: "contactbook" });
      } catch (error) {
        console.log(error);
        this.message = "Đã xảy ra lỗi khi thêm một liên hệ mới!";
      }
    },
  },
};
</script>
