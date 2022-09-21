<template>
  <div class="h-[800px]">
    <HeaderTitle />
    <div class="pt-5 flex justify-center">
      <table class="ml-4 border-2 border-black w-[720px]">
        <TableTitle />
        <div
          v-for="(judul, index) in julud"
          :key="'urutan-judul' + judul.id"
          class="font-medium"
        >
          <div class="flex">
            <p class="pl-7 w-[66px] font-mono border-r-2 border-black">
              {{ index + 1 }}
            </p>
            <p class="pl-2 w-[486px] font-mono text-slate-800">
              {{ judul.title }}
            </p>
            <div class="border-l-2 border-black pt-1 pb-1">
              <button
                type="edit"
                name="edit"
                class="border rounded-lg border-transparent bg-sky-500 py-1 px-2 shadow-xl font-mono hover:text-white hover:border-sky-700 hover:bg-sky-700 transition duration-500 ease-in-out ml-2"
                @click="edit(judul.id)"
              >
                edit
              </button>
              <button
                type="delete"
                name="delete"
                class="border rounded-lg border-transparent bg-red-500 py-1 px-2 shadow-xl font-mono hover:text-white hover:border-red-700 hover:bg-red-700 transition duration-500 ease-in-out ml-2"
                @click="hapus(judul.id)"
              >
                delete
              </button>
            </div>
          </div>
        </div>
      </table>
    </div>
    <div class="pt-6 flex justify-center">
      <button
        class="py-1 px-2 font-mono font-medium border border-slate-400 rounded-lg flex justify-center items-center opacity-80 hover:opacity-90 hover:border-white hover:bg-slate-300 transition duration-300 ease-in-out"
        @click="popupon = true"
      >
        Add New Title
      </button>
    </div>
    <form
      v-if="popupon"
      class="flex items-center justify-center fixed inset-0 bg-black/50 z-10"
      @submit.prevent="save"
    >
      <div
        class="w-[270px] h-[80px] opacity-90 border border-sky-400 bg-sky-400 rounded-lg shadow-xl"
      >
        <div class="p-18 flex justify-end">
          <div class="w-5 h-5 rounded-full">
            <span
              class="text-3xl m-auto hover:text-slate-700 transition duration-500 ease-in-out cursor-pointer"
              @click="popupon = false"
            >
              &times;
            </span>
          </div>
        </div>
        <h2 class="mr-2">Add Title :</h2>
        <input v-model="form.id" type="hidden" name="id" value="" />
        <input
          v-model="form.title"
          type="text"
          name="title"
          value=""
          class="border-2 border-black"
        />
        <button
          v-show="!updateSubmit"
          type="submit"
          name="add"
          class="border rounded-lg border-transparent bg-slate-300 py-1 px-2 shadow-xl font-mono hover:text-white hover:border-slate-700 hover:bg-slate-700 transition duration-500 ease-in-out ml-2"
        >
          Simpan
        </button>
        <button
          v-show="updateSubmit"
          type="button"
          name="update"
          class="border rounded-lg border-transparent bg-slate-300 py-1 px-2 shadow-xl font-mono hover:text-white hover:border-slate-700 hover:bg-slate-700 transition duration-500 ease-in-out ml-2"
          @click="update(form)"
        >
          Update
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      form: {
        id: '',
        title: '',
      },
      julud: [],
      updateSubmit: false,
      popupon: false,
      error: '',
    }
  },
  async fetch() {
    await this.titles()
  },

  methods: {
    async titles() {
      try {
        const res = await this.$axios.get(
          'https://jsonplaceholder.typicode.com/posts/'
        )
        this.julud = res.data.slice(0, 5)
      } catch (err) {
        this.error = 'Error'
      }
      // this.$axios
      //   .get('https://jsonplaceholder.typicode.com/posts',{
      //     title: this.title,
      //     userId: 1
      //   }).then(function(data){
      //     console.log(data);
      //   });
    },
    async save() {
      try {
        const res = await this.$axios.post(
          'https://jsonplaceholder.typicode.com/posts/',
          this.form
        )
        this.julud = res.data
        alert('Succeed')
      } catch (err) {
        this.error = 'Error'
      }
    },
    edit(id, title) {
      this.updateSubmit = true
      this.form.id = id
      this.form.title = title
      this.popupon = true
    },
    async update(form) {
      try {
        const res = await this.$axios.put(
          'https://jsonplaceholder.typicode.com/posts/' + form.id
        )
        this.julud = res.data
        this.updateSubmit = false
        alert('Succeed')
      } catch (err) {
        this.error = 'Error'
      }
    },
    async hapus(id) {
      try {
        // await this.$axios.delete(
        //   'https://jsonplaceholder.typicode.com/posts/1' + judul.id
        // )
        const res = await this.$axios.delete(
          'https://jsonplaceholder.typicode.com/posts/' + id
        )
        this.julud = res.data
        alert('Succeed')
        // console.log(res.data)
      } catch (err) {
        this.error = 'Error'
      }
    },
  },
}
</script>
