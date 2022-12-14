<script>
export default {
  name: "RowTableCategories",
  data() {
    return {};
  },
  props: ["data", "index"],
};
</script>

<template>
  <tr>
    <th class="fw-bold mb-1">{{ index + 1 }}</th>
    <td>{{ data.name }}</td>
  </tr>
</template>
