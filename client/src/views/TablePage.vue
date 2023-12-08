<script>
import RowTableAdvertisement from "../components/RowTableAdvertisement.vue";

export default {
  name: "TablePage",
  components: {
    RowTableAdvertisement,
  },
  props: ["dataAdvertisement", "page"],
  emits: ["getAdvertisementId", "statusAdvertisement"],
  methods: {
    getAdvertisementId(id) {
      this.$emit("getAdvertisementId", id);
    },
    statusAdvertisement(status, id) {
      this.$emit("statusAdvertisement", status, id);
    },
  },
  components: { RowTableAdvertisement},
};
</script>

<template>
  <div class="row">
    <div class="col">
      <div class="table-responsive">
        <!-- tabel Advertisement -->
        <table v-if="page === 'Advertisement'" class="table bg-white rounded border">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Title</th>
              <th scope="col">Description</th>
              <th scope="col">Price</th>
              <th scope="col">Stock</th>
              <th scope="col">Images</th>
              <th scope="col">Category</th>
              <th scope="col">Author</th>
              <th scope="col">Status</th>
              <th scope="col"></th>
            </tr>
          </thead>
          <tbody>
            <RowTableAdvertisement
              v-for="(Advertisement, index) in dataAdvertisement"
              :key="index"
              :data="Advertisement"
              :index="index"
              @getAdvertisementId="getAdvertisementId"
              @statusAdvertisement="statusAdvertisement"
            />
          </tbody>
        </table>
        <!-- tabel history -->
        <table
          v-else-if="page === 'history'"
          class="table bg-white rounded border"
        >
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Name</th>
              <th scope="col">Description</th>
              <th scope="col">Created At</th>
              <th scope="col">Update By</th>
              <th scope="col"></th>
            </tr>
          </thead>
          <tbody>
            <RowTableHistory
              v-for="(history, index) in dataHistory.data"
              :key="index"
              :data="history"
              :index="index"
            />
          </tbody>
        </table>
        <!-- table category -->
        <table
          v-else-if="page === 'category'"
          class="table bg-white rounded border"
        >
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Name</th>
              <th scope="col"></th>
            </tr>
          </thead>
          <tbody>
            <RowTableCategory
              v-for="(category, index) in dataCategory"
              :key="index"
              :data="category"
              :index="index"
            />
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>