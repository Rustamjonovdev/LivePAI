<template>
  <div class="bg-[#111827] p-4">
    <nav>
      <ul
        class="border-2 border-gray-700 rounded-xl flex justify-between items-center p-2"
      >
        <li>
          <img
            src="./assets/img/svg/logo.jpg"
            alt="Logo image"
            class="logo h-[25px] w-[50px] rounded-sm shadow-lg shadow-blue-500/50"
          />
        </li>
        <li>
          <router-link to="/"
            ><h1 class="Title text-2xl font-bold text-white">
              LivePAI
            </h1></router-link
          >
        </li>
        <li>
          <Router-Link
            to="/login"
            class="bg-[#3b82f6] text-white font-bold p-[6px] rounded-sm hover:bg-[#2563eb]"
          >
            Login
          </Router-Link>
        </li>
      </ul>
    </nav>
    <main>
      <router-view />
    </main>
    <footer
      class="border-2 border-gray-700 rounded-xl flex justify-between p-8"
    >
      <div>
        <img src="./assets/img/png/logo.png" class="h-[72px]" alt="Logo" />
      </div>
      <ul class="costumers text-white">
        <li>Tuzuvchi</li>
        <li>Texnik yordam</li>
        <li>Manzil</li>
      </ul>
      <ul class="social flex flex-col gap-2">
        <li class="flex items-center gap-2 hover:cursor-pointer">
          <img
            src="./assets/img/svg/instagram-brands.svg"
            alt="instagram"
            class="h-[16px]"
          />
          <h4 class="text-sm text-white">Instagram</h4>
        </li>
        <li class="flex items-center gap-2 hover:cursor-pointer">
          <img
            src="./assets/img/svg/telegram-brands.svg"
            alt="telegram-icons"
            class="h-[16px]"
          />
          <h3 class="text-sm text-white">Telegram</h3>
        </li>
        <li class="flex items-center gap-2 hover:cursor-pointer">
          <img
            src="./assets/img/svg/youtube-brands.svg"
            alt="you tube"
            class="h-[16px]"
          />
          <h3 class="text-sm text-white">You tube</h3>
        </li>
      </ul>
    </footer>
  </div>
</template>

<script setup></script>
