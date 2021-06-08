<template>
<v-app>
    <h1>This is Home</h1>
    <p>This is the Title: {{title}} and this the number {{number}}</p>
    <Nuxt />
    <NuxtLink to="/login">To the Login</NuxtLink>
</v-app>
</template>

<script lang="ts">
import {Vue,Component} from "vue-property-decorator"

// Boring without TypeScript
// export default {
//     data(){
//         return {
//             title: 'HomePage',
//             number: 69
//         }
//     }
// }

@Component
export default class IndexClass extends Vue {
    number = 69;
    title = 'TitlePage';
}
</script>

<style>

</style>