<template>
  <div class="home">
    <div class="container">
      <input-contact-form
        title="Devcode Contact Manager"
        :selectedContact="selectedContact"
        :isEdit="isEdit"
      />
      <div class="contact-list__container">
        <contact-item
          v-for="contact in contactsData"
          :key="contact.id"
          :id="contact.id"
          :full_name="contact.full_name"
          :phone_number="contact.phone_number"
          :email="contact.email"
        />
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import InputContactForm from "@/components/InputContactForm.vue";
import ContactItem from "@/components/ContactItem.vue";

export default {
  name: "HomeView",
  components: {
    InputContactForm,
    ContactItem,
  },
  data() {
    return {
      contactsData: [],
      selectedContact: {
        id: 0,
        full_name: "",
        phone_number: "",
        email: "",
      },
      isEdit: false,
    };
  },
  mounted() {
    this.getAllContactsData();
  },
  methods: {
    setSelectedData(id, name, phone, email) {
      this.selectedContact.id = id;
      this.selectedContact.full_name = name;
      this.selectedContact.phone_number = phone;
      this.selectedContact.email = email;
      this.isEdit = true;
    },
    resetSelectedData() {
      this.selectedContact.id = 0;
      this.selectedContact.full_name = "";
      this.selectedContact.phone_number = "";
      this.selectedContact.email = "";
      this.isEdit = false;
    },
    async getAllContactsData() {
      const response = await this.$store.dispatch("getAllContactsData");
      this.contactsData = response.data.data;
    },
  },
};
</script>

<style lang="scss" scoped>
.home {
  display: flex;
  justify-content: center;

  .container {
    padding: 18px;
    width: 50%;
    height: 100%;
    border: solid 4px #d4d4d4;
    background: #f4f4f4;

    .contact-list {
      &__container {
        margin-top: 48px;
        display: flex;
        flex-direction: column;
        align-items: center;
      }
    }
  }
}
</style>
