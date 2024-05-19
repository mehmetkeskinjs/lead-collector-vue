<template>
    <div class="pt-5">
        <h1 class="text-4xl text-cyan-950 text-center font-bold">Create Form</h1>

        <form ref="form" class="flex flex-col gap-3 w-[500px] mx-auto mt-5 border shadow-sm rounded-lg p-4">
            <div class="flex flex-col gap-2">
                <label for="firstName">First Name</label>
                <input 
                    class="w-full h-10 flex items-center justify-center border shadow-sm rounded-md px-4" 
                    type="text" 
                    id="firstName"
                    v-model="form.firstName">
            </div>

            <div class="flex flex-col gap-2">
                <label for="lastName">Last Name</label>
                <input 
                    class="w-full h-10 flex items-center justify-center border shadow-sm rounded-md px-4" 
                    type="text" 
                    id="lastName"
                    v-model="form.lastName">
            </div class="flex flex-col gap-2">

            <div class="flex flex-col gap-2">
                <label for="birthDay">Birthday</label>
                <input 
                    class="w-full h-10 flex items-center justify-center border shadow-sm rounded-md px-4" 
                    type="date" 
                    id="birthDay"
                    v-model="form.birthDay">
            </div>

            <div class="flex flex-col gap-2">
                <label for="country">Country</label>
                <select 
                    class="w-full h-10 flex items-center justify-center border shadow-sm rounded-md px-4"
                    id="country"
                    v-model="form.country">
                        <option v-for="(country, index) in countries" :key="index" :value="country">{{ country }}</option>
                </select>
            </div>

            <div class="flex flex-row-reverse items-center justify-end gap-2">
                <label for="acknowledgement">Check this box</label>
                <input
                    type="checkbox"
                    id="acknowledgement"
                    v-model="form.acknowledgement">
            </div>

            <button 
                class="w-full h-10 bg-cyan-950 text-gray-50 rounded-md disabled:bg-gray-100 disabled:text-gray-800 disabled:cursor-not-allowed"
                :disabled="!isButtonDisabled"
                @click="submitForm()">
                Submit
            </button>
        </form>
    </div>
</template>

<script>
export default {
    name: "Create New Form",

    computed: {
        isButtonDisabled() {
            const { firstName, lastName, birthDay, country, acknowledgement } = this.form;

            return firstName && lastName && birthDay && country && acknowledgement;
        }
    },

    data() {
        return {
            countries: ["Turkey", "Switzerland", "France"],
            form: {
                firstName: '',
                lastName: '',
                birthDay: undefined,
                country: '',
                acknowledgement: false
            }
        }
    },

    methods: {
        submitForm() {
            event.preventDefault();

            const formData = JSON.parse(localStorage.getItem('formData')) || [];

            formData.push(this.form);
            localStorage.setItem('formData', JSON.stringify(formData));

            this.$refs.form.reset();
        }
    }
}
</script>

<style scoped>
</style>
  