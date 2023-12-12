<script setup>
import { ref } from "vue";

const nom = ref("");
const email = ref("");
const message = ref("");

const submitForm = () => {
    const dataToSend = {
        content: `nom: ${nom.value}\nemail: ${email.value}\nmessage: ${message.value}`,
    };

    sendToDiscord(dataToSend);

    resetForm();
};

const sendToDiscord = (data) => {
    fetch(
        "https://discord.com/api/webhooks/1182481776015331368/bqTIG__3a9Qeibkq0bXC13eaej0D6VZR1Eeqc_W1YNu69LkC2dCNVbhS9A6yUiHCFpet",
        {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify(data),
        }
    )
        .then((response) => {
            if (!response.ok) {
                throw new Error("Error sending data to Discord webhook");
            }
        })
        .catch((error) => {
            console.error(error);
            // Handle errors here
        });
};

const resetForm = () => {
    nom.value = "";
    email.value = "";
    message.value = "";
};
</script>

<template>
    <form
        @submit.prevent="submitForm"
        class="border-2 border-[orange] p-2 flex gap-2 flex-col"
    >
        <h1 class="font-bold text-[2rem]">Contact</h1>

        <div class="flex gap-2">
            <label for="nom">Nom:</label>
            <input
                class="border-2 border-[black]"
                type="text"
                id="nom"
                v-model="nom"
                required
            />
        </div>

        <div class="flex gap-2">
            <label for="email">Email:</label>
            <input
                class="border-2 border-[black]"
                type="email"
                id="email"
                v-model="email"
                required
            />
        </div>

        <div class="flex gap-2">
            <label for="message">Message:</label>
            <textarea
                class="border-2 border-[black]"
                id="message"
                v-model="message"
                required
            ></textarea>
        </div>

        <button type="submit">Envoyer</button>
    </form>
</template>

<style scoped></style>
