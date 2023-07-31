<template>
  <q-page>
    <div class="q-pa-md">
      <q-table
        class="my-sticky-header-table"
        flat
        bordered
        separator="cell"
        title="Database"
        :rows="posts"
        :columns="columns"
        :rows-per-page-options="[30, 60, 600]"
        row-key="name"
      />
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref, onMounted } from "vue";
import { api } from "boot/axios";

export default defineComponent({
  name: "IndexPage",
  setup() {
    const posts = ref([]);
    const columns = [
      {
        name: "name",
        field: "name",
        label: "Nome",
        sortable: true,
        align: "left",
      },
      {
        name: "house",
        field: "house",
        label: "Casa",
        sortable: true,
        align: "left",
      },
      {
        name: "actor",
        field: "actor",
        label: "Ator",
        sortable: true,
        align: "left",
      },
      {
        name: "gender",
        field: "gender",
        label: "Gênero",
        sortable: true,
        align: "left",
      },
      {
        name: "species",
        field: "species",
        label: "Raça",
        sortable: true,
        align: "left",
      },
      /* {
        name: "patronus",
        field: "patronus",
        label: "Patrono",
        sortable: true,
        align: "left",
      },*/
      {
        name: "yearOfBirth",
        field: "yearOfBirth",
        label: "Nascimento",
        sortable: true,
        align: "left",
      },
    ];

    onMounted(() => {
      getPosts();
    });

    const getPosts = async () => {
      try {
        const { data } = await api.get("characters");
        posts.value = data;
        console.log(data);
      } catch (error) {
        console.error(error);
      }
    };

    return {
      posts,
      columns,
      filter: ref(""),
    };
  },
});
</script>

<style lang="sass">
.my-sticky-header-table
  height: 85vh

  .q-table__top,
  .q-table__bottom,
  thead tr:first-child th
    color: white
    background-color: $primary

  thead tr th
    position: sticky
    z-index: 1
    background-color: $secondary !important
  thead tr:first-child th
    top: 0

  &.q-table--loading thead tr:last-child th
    top: 48px

  tbody
    scroll-margin-top: 48px

  .q-field__native span, .q-table__control span,  .q-field__append i
    color: white

  .custom-caption
    text-align: center
    padding: 12px
    color: white
    background-color: rgba(0, 0, 0, .3)
</style>
