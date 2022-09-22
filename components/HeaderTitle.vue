<template>
  <header>
    <nav class="bg-white shadow">
      <div class="container px-6 py-3 mx-auto">
        <div class="md:flex justify-between items-center">
          <!-- left section -->
          <div class="flex justify-between items-center">
            <a
              href="#"
              class="text-gray-800 text-xl text-slate-500 font-medium hover:text-gray-700 md:text-2xl"
              >Book<span class="text-sky-500">shelf</span></a
            >
            <div class="flex absolute right-8">
              <button
                type="button"
                class="text-gray-500 hover:text-gray-600 focus:text-gray-600 focus:outline-none"
                @click="isOpen = !isOpen"
              >
                <svg viewBox="0 0 24 24" class="h-6 w-6 fill-current">
                  <path
                    d="M4 5h16a1 1 0 0 1 0 2H4a1 1 0 1 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2z"
                  ></path>
                </svg>
              </button>
            </div>
          </div>
          <!-- right section -->
          <div class="flex relative mt-1" :class="isOpen ? 'flex' : 'hidden'">
            <a href="#" class="text-gray-800 text-sm hover:font-medium md:mx-4"
              >Home</a
            >
            <a
              href="books"
              class="text-gray-800 text-sm hover:font-medium md:mx-4"
              >Table Books</a
            >
            <a href="#" class="text-gray-800 text-sm hover:font-medium md:mx-4"
              >Login</a
            >
          </div>
        </div>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'HeaderTitle',
  data() {
    return {
      isOpen: false,
    }
  },
}
</script>
