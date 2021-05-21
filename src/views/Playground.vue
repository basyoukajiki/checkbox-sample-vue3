<template>
  <div class="about">
    <h1>Playgroundページ</h1>
    <!-- ↓全選択用のチェックボックス -->
    <Checkbox 
      v-model="allChecked"
    />
    <div v-for="(user, key) in userData" :key="key">
      <Checkbox
        v-model="checkedItems"
        :value="user.id"
        :label="user.name"
      />
    </div>
    <h2>↓checkedItems↓</h2>
    <p>{{ checkedItems }}</p>
  </div>
</template>
<script lang="ts">
import { defineComponent, ref, computed } from "vue";
import Checkbox from "@/components/Checkbox.vue";

export default defineComponent({
  components: {
    Checkbox
  },
  setup() {
    const userData = ref([
      {
        id: 1,
        name: "hoge",
        email: "hoge@email.com"
      },
      {
        id: 2,
        name: "bar",
        email: "bar@email.com"
      },
      {
        id: 3,
        name: "Baz",
        email: "baz@email.com"
      }
    ]);

    const checkedItems = ref<number[]>([]);
    const allChecked = computed({
      get: () => checkedItems.value.length === userData.value.length,
      set: (v) => {
        if (v) {
          console.log(v);
          checkedItems.value = userData.value.map((r) => r.id);
        } else {
          console.log(v);
          checkedItems.value = [];
        }
      }
    });
    return {
      userData,
      checkedItems,
      allChecked
    };
  }
});
</script>
<style scoped></style>
