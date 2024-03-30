<template>
    <div class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactForm
            :contact="newContact"
            @submit:contact="addContact"
        />
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
            newContact: {
                name: '',
                email: '',
                address: '',
                phone: '',
                favorite: false
            },
            message: "",
        };
    },
    methods: {
        async addContact(data) {
            try {
                await ContactService.create(data);
                this.message = "Liên hệ được thêm thành công.";
                this.newContact = {
                    name: '',
                    email: '',
                    address: '',
                    phone: '',
                    favorite: false
                };
            } catch (error) {
                console.log(error);
            }
        },
    },
};
</script>
