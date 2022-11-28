<template>
    <div>
        <div class="col-md-12">
            <table class="table table-light ">
                <thead class="bg-warning">
                    <tr>
                        <th>Ações</th>
                        <th>Nome</th>
                        <th>Email</th>
                        <th>Sexo</th>
                        <th>Telefone</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="contact in contacts" :key="contact.id">
                        <td>
                            <button class="btn btn-sm btn-primary mr-1" @click="editContact(contact)"><i class="fa fa-edit"></i></button>
                            <button class="btn btn-sm btn-danger" @click="deleteContact(contact)"><i class="fas fa-trash"></i></button>
                        </td>
                        <td>{{ contact.nome }}</td>
                        <td>{{ contact.email }}</td>
                        <td>{{ contact.sexo }}</td>
                        <td>{{ contact.telefone }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
        <div class="col-md-12">
            <form-contacts ref="form"/>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import FormContacts from "@/components/FormContacts";

export default {
    name: 'ListContacts',
    components: {
        FormContacts
    },
    data() {
        return {
            contacts: [],
            route: 'https://contacts-api-rest.herokuapp.com/api/contacts'
        }
    },
    mounted() {
        this.listContacts(this.route)
    },
    methods: {
        listContacts(route) {
            axios.get(route)
                .then(res => {
                    console.log(res.data);
                    this.contacts = Object.values(res.data)
                });
        },
        editContact(contact) {
            this.$refs.form.edit(contact)
        },
        deleteContact(contact) {
            this.$refs.form.deleteContact(contact)
        }
    }
}
</script>
