<template>
  <div class="wrapper-content wrapper-content--fixed">
    <section>
      <div class="container">
        <!-- table -->
        <table>
          <!-- head -->
          <thead>
            <tr>
              <th @click="sort('name')">Name &#8595;</th>
              <th @click="sort('age')">Age &#8595;</th>
              <th @click="sort('gender')">Gender &#8595;</th>
            </tr>
          </thead>
          <!-- body -->
          <tbody>
            <tr v-for="user in usersSort" :key="user.id">
              <td>
                <img :src="user.img" :alt="user.name" />
                <span>{{ user.name }}</span>
              </td>
              <td>{{ user.age }}</td>
              <td>{{ user.gender }}</td>
            </tr>
          </tbody>
        </table>
        <p style="text-align:center;">
          <span>debug: sort: {{ currentSort }}, dir: {{ currentSortDir }}</span>
          <span>
            page: {{ this.page.current }}, length: {{ this.page.length }}</span
          >
        </p>
      </div>
    </section>
    <!-- buttons -->
    <section>
      <div class="container">
        <div class="button-list">
          <div class="btn btnPrimary" @click="prevPage">&#8592;</div>
          <div class="btn btnPrimary" @click="nextPage">&#8594;</div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      users: [],
      currentSort: "name",
      currentSortDir: "asc",
      page: {
        current: 1,
        length: 5,
      },
    };
  },
  created() {
    // https://randomuser.me/api/?results=20
    //
    // axios
    //   .get("https://api.myjson.com/bin/rzgya")
    //   .then((Response) => {
    //     //console.log(Response.data);
    //     this.users = Response.result;
    //   })
    //   .catch((error) => {
    //     console.log(error);
    //   });
    this.users = [
      {
        id: 1,
        name: "Jack",
        age: 22,
        gender: "male",
        img: "https://randomuser.me/api/portraits/med/men/74.jpg",
      },
      {
        id: 2,
        name: "Alex",
        age: 24,
        gender: "male",
        img: "https://randomuser.me/api/portraits/med/men/75.jpg",
      },
      {
        id: 3,
        name: "John",
        age: 28,
        gender: "male",
        img: "https://randomuser.me/api/portraits/med/men/73.jpg",
      },
      {
        id: 4,
        name: "Helen",
        age: 34,
        gender: "female",
        img: "https://randomuser.me/api/portraits/med/women/75.jpg",
      },
      {
        id: 5,
        name: "Kate",
        age: 24,
        gender: "female",
        img: "https://randomuser.me/api/portraits/med/women/74.jpg",
      },
      {
        id: 6,
        name: "Morgan",
        age: 31,
        gender: "male",
        img: "https://randomuser.me/api/portraits/med/men/71.jpg",
      },
      {
        id: 7,
        name: "Fred",
        age: 37,
        gender: "male",
        img: "https://randomuser.me/api/portraits/med/men/72.jpg",
      },
      {
        id: 8,
        name: "Harry",
        age: 44,
        gender: "male",
        img: "https://randomuser.me/api/portraits/med/men/76.jpg",
      },
      {
        id: 9,
        name: "Dave",
        age: 19,
        gender: "male",
        img: "https://randomuser.me/api/portraits/med/men/77.jpg",
      },
    ];
  },
  computed: {
    usersSort() {
      return this.users
        .sort((a, b) => {
          let mod = 1;
          if (this.currentSortDir === "desc") mod = -1;
          if (a[this.currentSort] < b[this.currentSort]) return -1 * mod;
          if (a[this.currentSort] > b[this.currentSort]) return 1 * mod;
          return 0;
        })
        .filter((row, index) => {
          let start = (this.page.current - 1) * this.page.length;
          let end = this.page.current * this.page.length;
          if (index >= start && index < end) return true;
        });
    },
  },
  methods: {
    sort(e) {
      if (e === this.currentSort) {
        this.currentSortDir = this.currentSortDir === "asc" ? "desc" : "asc";
      }
      this.currentSort = e;
    },
    nextPage() {
      if (this.page.current * this.page.length < this.users.length)
        this.page.current += 1;
    },
    prevPage() {
      if (this.page.current > 1) this.page.current -= 1;
    },
  },
};
</script>

<style lang="scss" scoped>
img {
  width: 60px;
  height: auto;
  border-radius: 50%;
  margin-right: 16px;
}
.button-list {
  width: 100%;
  text-align: center;
  .btn {
    border-radius: 60px;
    margin: 0 20px;
  }
}
</style>
