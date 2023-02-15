<template>
  <main class="main-container">
    <!-- <UserMsg /> -->
    <RouterLink to="/contact/edit"><button>Add Contact</button></RouterLink>
    <ContactList v-if="contacts" :contacts="contacts" @remove="removeContact" />
  </main>
</template>

<script>
import { contactService } from "@/services/contactService.js";
import ContactList from "@/cmps/contact-list.vue";

export default {
  data() {
    return {
      contacts: null,
    };
  },
  methods: {
    async removeContact(contactId) {
      console.log("contactId", contactId);

      const msg = {
        txt: `contact ${contactId} deleted.`,
        type: "success",
        timeout: 2500,
      };
      await contactService.deleteContact(contactId);
      this.contacts = this.contacts.filter(
        (contact) => contact._id !== contactId
      );
      //   eventBus.emit("user-msg", msg);
    },
    async addContact(contact) {},
  },
  async created() {
    this.contacts = await contactService.getContacts();
    // console.log(this.contacts);
  },
  components: {
    ContactList,
  },
};
</script>

<style>
</style>