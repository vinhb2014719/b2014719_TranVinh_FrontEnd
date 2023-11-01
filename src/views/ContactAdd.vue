<template>
    <div v-if="contact" class="page">
        <h4>Hiệu chỉnh Liên hệ</h4>
        <ContactForm
            :contact="contact"
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
    props: {
        id: { type: String, required: true },
    },
    data() {
        return {
            contact: {
                name: "",
                email: "",
                addpress: "",
                phone: "",
                favorite: "",
            },
            message: "",
        };
    },
    methods: {
        
        async addContact(data) {
            try {
                await ContactService.create(data);
                this.message = "Liên hệ được cập nhật thành công.";
            } catch (error) {
                console.log(error);
                this.message = "Đã xảy ra lỗi.";
            }
        },
    },   
};
</script>