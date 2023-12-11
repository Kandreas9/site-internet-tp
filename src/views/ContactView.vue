<script setup>
import { ref } from "vue";

const nom = ref("");
const email = ref("");
const message = ref("");

const submitForm = () => {
    const dataToSend = {
        nom: nom.value,
        email: email.value,
        content: message.value,
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
    <form @submit.prevent="submitForm">
        <label for="nom">Nom:</label>
        <input type="text" id="nom" v-model="nom" required />

        <label for="email">Email:</label>
        <input type="email" id="email" v-model="email" required />

        <label for="message">Message:</label>
        <textarea id="message" v-model="message" required></textarea>

        <button type="submit">Envoyer</button>
    </form>
</template>

<style scoped></style>
