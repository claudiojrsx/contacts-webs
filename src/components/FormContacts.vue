<template>
    <div class="mt-5 rounded bg-pink">
        <h4>Cadastro de Contatos</h4>
        <form id="form-contacts">
            <label for="">Nome</label>
            <div class="form-group">
                <input type="text" name="nome" id="nome" class="form-control" required>
            </div>
            <label for="">Email</label>
            <div class="form-group">
                <input type="mail" name="email" id="email" class="form-control" required placeholder="exemplo@exemplo.com">
            </div>
            <label for="">Sexo</label>
            <div class="form-group">
                <select class="form-control" name="sexo" id="sexo">
                    <option value="Masculino">M</option>
                    <option value="Feminino">F</option>
                </select>
            </div>
            <label for="">Telefone</label>
            <div class="form-group">
                <input type="text" id="telefone" name="telefone" class="form-control" required placeholder="(92) 99999-9999">
            </div>
            <button class="btn btn-outline-success" @click="saveContact">Salvar</button>
        </form>
    </div>
</template>

<script>
import axios from "axios";

export default {
    name: "FormContacts",
    data() {
        return {
            contact: [],
            route: 'https://contacts-api-rest.herokuapp.com/api/contacts'
        }
    },
    methods: {
        saveContact() {
            let method = null
            let data = {}
            if (this.contact) {
                method = "put"
                data = {
                    id: this.contact.id,
                    nome: document.getElementById('nome').value,
                    email: document.getElementById('email').value,
                    sexo: document.getElementById('sexo').value,
                    telefone: document.getElementById('telefone').value,
                }
            } else {
                method = "post"
                data = {
                    nome: document.getElementById('nome').value,
                    email: document.getElementById('email').value,
                    sexo: document.getElementById('sexo').value,
                    telefone: document.getElementById('telefone').value,
                }
            }
            axios({
                method: method,
                url: this.route,
                data: data,
                headers: { 'content-type': 'application/json' }
            })
                .then(res => {
                    console.log(res.data);
                    window.reload()
                });
        },
        edit(contact) {
            this.contact = contact
            document.getElementById('nome').value = contact.nome
            document.getElementById('email').value = contact.email
            document.getElementById('sexo').value = contact.sexo
            document.getElementById('telefone').value = contact.telefone
        },
        deleteContact(contact) {
            let data = {
                id: contact.id,
                nome: contact.nome,
                email: contact.email,
                sexo: contact.sexo,
                telefone: contact.telefone,
            }
            
            axios({
                method: "delete",
                url: this.route,
                data: data,
                headers: { 'content-type': 'application/json' }
            })
                .then(res => {
                    console.log(res.data);
                    window.reload()
                });
        },
    }
}
</script>

<style>

</style>