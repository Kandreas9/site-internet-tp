<script setup>
import { ref } from "vue";

const apiUrl = ref("");
const method = ref("GET");
const parameter = ref("");
const apiResult = ref(null);

const callApi = () => {
    fetch(`${apiUrl.value}?${parameter.value}`, {
        method: method.value,
        headers: {
            "Content-Type": "application/json",
        },
    })
        .then(async (res) => {
            if (!res.ok) {
                throw new Error("Error sending data to Discord webhook");
            }

            const responseData = await res.json();

            apiResult.value = responseData;
        })
        .catch((err) => {
            console.error(err);
        });
};
</script>

<template>
    <div class="flex justify-between p-2 border-2 border-[orange]">
        <form class="flex-col flex gap-2" @submit.prevent="callApi">
            <h1>Contacter une API</h1>

            <div>
                <label for="api-url">URL:</label>
                <input
                    class="border-2 border-[black]"
                    type="text"
                    id="api-url"
                    v-model="apiUrl"
                />
            </div>

            <div>
                <label for="method">Méthode:</label>
                <select
                    class="border-2 border-[black]"
                    id="method"
                    v-model="method"
                >
                    <option value="GET">GET</option>
                    <option value="POST">POST</option>
                </select>
            </div>

            <div>
                <label for="parameter">Paramètre:</label>
                <input
                    class="border-2 border-[black]"
                    type="text"
                    id="parameter"
                    v-model="parameter"
                />
            </div>

            <button type="submit">Call API</button>
        </form>

        <div>
            <p>API Result:</p>
            <pre
                class="overflow-auto border-2 border-[black] h-[20rem] w-[30rem]"
                >{{ apiResult }}</pre
            >
        </div>
    </div>
</template>
