<script setup lang="ts">
import DigitView from "./components/digitView.vue";
</script>

<template>
  <div style="width: 100%; padding: 12px 0">
    <digit-view 
        style="
					width: 98%;
					margin-left: 1%;
					min-width: 1080px;
				"
        num='00110011001100110011001100110011'
        :start=0 />
  </div>
</template>