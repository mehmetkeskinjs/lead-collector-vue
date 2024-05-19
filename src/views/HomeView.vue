<template>
    <div>
        <header class="bg-cyan-300 bg-opacity-5">
            <ul class="flex justify-between items-center text-cyan-900 text-lg font-bold p-4">
                <li class="pl-4">First Name</li>
                <li>Last Name</li>
                <li>BirthDay</li>
                <li class="pr-4">Country</li>
            </ul>
        </header>
        <main>
            <div v-if="this.items.length === 0">
                <p class="text-gray-400 text-center pt-4"> No Data to show </p>
            </div>
            <div v-else>
                <div class="flex justify-between items-center p-4"
                    v-for="(item, index) in items" :key="index">
                    <div>{{ index + 1 }}. {{ item.firstName }}</div>
                    <div>{{ item.lastName }}</div>
                    <div>{{ item.birthDay }}</div>
                    <div>
                        {{ item.country }} 
                        <button class="bg-red-500 text-white rounded-md p-2"
                            @click="deleteItem(index)">
                                Delete
                        </button>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <RouterLink class="fixed bottom-12 right-12 bg-cyan-950 text-neutral-50 text-lg rounded-full px-5 py-2"
                to="/new-form">
        Create a New Form
    </RouterLink>
</template>

<script>
export default {
    name: 'Forms',

    data() {
        return {
            items: [],
        }
    },

    methods: {
        deleteItem(index) {
            this.items.splice(index, 1)

            localStorage.setItem('formData', JSON.stringify(this.items))
        }
    },

    mounted() {
        this.items = JSON.parse(localStorage.getItem('formData'));
    }
}
</script>  