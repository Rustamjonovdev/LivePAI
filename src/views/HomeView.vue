<template>
  <div>
    <div class="main grid grid-cols-2 gap-2 p-4 h-full">
      <div class="work-part border-2 border-gray-700 rounded-xl m-4 gap-8 p-2">
        <h1 class="text-2xl text-white font-bold flex justify-center">
          Rasmni tanlang
        </h1>
        <!-- Custom file input button -->
        <div class="flex flex-col items-center h-[500px] gap-4 pt-[70px]">
          <button
            class="Choose_file bg-[#3b82f6] h-[20%] w-[90%] text-4xl font-medium text-white rounded-xl hover:cursor-pointer hover:bg-[#2563eb]"
            @click="openFilePicker"
          >
            +
          </button>
          <!-- Hidden file input -->
          <input
            type="file"
            accept="image/*"
            ref="fileInput"
            class="hidden"
            @change="handleFileChange"
          />

          <!-- Prompt input -->
          <textarea
            v-model="prompt"
            class="w-[90%] h-[150px] bg-gray-700 p-2 text-white rounded-xl"
            placeholder="Prompt kiriting..."
          ></textarea>

          <!-- Submit button -->
          <button
            class="bg-[#3b82f6] text-white py-2 px-4 rounded hover:bg-blue-700 w-[90%]"
            @click="submitForm"
            :disabled="loading"
          >
            {{ loading ? "Yaratilmoqda..." : "🎬 Videoni yaratish" }}
          </button>
        </div>
      </div>

      <div
        class="result border-2 border-gray-700 rounded-xl flex flex-col items-center h-[650px] gap-8 m-4 p-2"
      >
        <h1 class="text-2xl text-white font-bold mb-4">Natija</h1>

        <img
          v-if="imagePreview"
          :src="imagePreview"
          alt="Tanlangan rasm"
          class="mb-4 max-w-[250px] rounded-xl shadow-lg shadow-blue-500/50"
        />

        <!-- <img
          src="../assets/img/svg/logo.jpg"
          alt="Tanlangan rasm"
          class="mb-4 max-w-[250px] rounded-xl"
        /> -->
        <video
          v-if="videoUrl"
          :src="videoUrl"
          controls
          class="mb-4 max-w-[250px] rounded-xl"
        ></video>

        <p v-if="error" class="text-red-500 mt-2">{{ error }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const fileInput = ref(null);
const imageFile = ref(null);
const imagePreview = ref(null);
const prompt = ref("");
const videoUrl = ref("");
const loading = ref(false);
const error = ref("");

function openFilePicker() {
  fileInput.value.click();
}

function handleFileChange(event) {
  const file = event.target.files[0];
  if (file && file.type.startsWith("image/")) {
    imageFile.value = file;
    imagePreview.value = URL.createObjectURL(file);
  } else {
    imagePreview.value = null;
    imageFile.value = null;
    alert("Iltimos, rasm faylini tanlang.");
  }
}

async function submitForm() {
  error.value = "";
  if (!imageFile.value || !prompt.value) {
    error.value = "Rasm va prompt to‘ldirilishi shart.";
    return;
  }

  const formData = new FormData();
  formData.append("image", imageFile.value);
  formData.append("prompt", prompt.value);

  loading.value = true;

  try {
    const response = await fetch(
      "https://team.fargenius.uz/api/ai/generate-video/",
      {
        method: "POST",
        body: formData,
      }
    );

    const data = await response.json();

    if (response.ok) {
      videoUrl.value = data.video_url;
    } else {
      error.value = data.detail || "Video yaratishda xatolik yuz berdi.";
    }
  } catch (err) {
    error.value = "Tarmoqda xatolik: " + err.message;
  } finally {
    loading.value = false;
  }
}
</script>

<style scoped></style>
