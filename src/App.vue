<template>
    <div>
        <font-awesome-icon icon="user-secret" />
        <div class="container">
            <list-contacts />
        </div>
    </div>
</template>

<script>
import ListContacts from './components/ListContacts.vue';

export default {
    name: 'App',
    components: {
        ListContacts
    }
}
</script>

<style>

</style>