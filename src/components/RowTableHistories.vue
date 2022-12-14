<script>
export default {
  name: "RowTableHistories",
  data() {
    return {};
  },
  props: ["data", "index"],
  computed: {
    getFormatDate() {
      return new Date(this.data.createdAt).toLocaleString();
    },
  },
};
</script>

<template>
  <tr>
    <th class="fw-bold mb-1">{{ index + 1 }}</th>
    <td>{{ data.name }}</td>
    <td>{{ data.description }}</td>
    <td>{{ getFormatDate }}</td>
    <td>{{ data.updatedBy }}</td>
  </tr>
</template>
