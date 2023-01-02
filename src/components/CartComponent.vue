<script lang="ts">
import { useUserStore } from "@/stores/user";
import type { RentalObjectTypeType, TagType } from "@/ts/rent.types";
export default {
  setup() {
    defineProps<{
      objectType: RentalObjectTypeType;
    }>();
    const userStore = useUserStore();
    return { userStore };
  },
  methods: {
    addToCart(objectType: RentalObjectTypeType) {
      //check if this type is already in cart
      if (
        this.userStore.shoppingCart.filter((x) => x.id == objectType.id)
          .length > 0
      ) {
        // increase count by one
        this.userStore.shoppingCart.filter((x) => x.id == objectType.id)[0]
          .count++;
      } else {
        // add type and add count = 1 to the object
        this.userStore.shoppingCart.push({ ...objectType, count: 1 });
      }
    },
    removeFromCart(objectType: RentalObjectTypeType) {
      if (
        this.userStore.shoppingCart.find((x) => x.id == objectType.id).count > 1
      ) {
        this.userStore.shoppingCart.find((x) => x.id == objectType.id).count--;
      } else {
        const index = this.userStore.shoppingCart.indexOf(
          this.userStore.shoppingCart.find((x) => x.id == objectType.id)
        );
        this.userStore.shoppingCart.splice(index, 1);
      }
    },}
};
</script>

<template></template>
