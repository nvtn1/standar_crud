<template>
  <div class="flex flex-row font-medium border-b-2 border-black">
    <h3 class="w-[66px] border-r-2 border-black flex justify-center">Number</h3>
    <h3 class="ml-2 border-r-2 border-black w-[480px] flex justify-center">
      Book Title
    </h3>
    <h3 class="ml-2 w-[150px] flex justify-center">Function</h3>
  </div>
</template>

<script>
export default {
  name: 'TableTitle',
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
      id: 0,
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
    edit(id, title) {
      this.updateSubmit = true
      this.form.id = id
      this.form.title = title
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
