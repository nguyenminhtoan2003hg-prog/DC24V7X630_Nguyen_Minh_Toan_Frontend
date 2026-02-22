<template>
  <div class="page">
    <h4>Thêm Liên hệ</h4>

    <ContactForm
      :contact="contact"
      @submit:contact="saveContact"
    />

    <p class="mt-3">{{ message }}</p>
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
      contact: {
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
    async saveContact(data) {
        try {
        await ContactService.create(data);

        this.message = "Thêm liên hệ thành công!";

        this.$router.push("/");
      
        } catch (error) {
        console.log(error);
        }
        },
    },
};
</script>

<style scoped>
.page {
  text-align: left;
  max-width: 750px;
}
</style>