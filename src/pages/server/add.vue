<template>
  <VContainer
    class="fill-height"
    fluid>
    <VRow justify="center">
      <VCol
        sm="6"
        md="6"
        lg="5">
        <AddServerForm />
      </VCol>
    </VRow>
  </VContainer>
</template>

<route lang="yaml">
meta:
  layout: server
</route>

<script setup lang="ts">
import { useI18n } from 'vue-i18n';
import { useRoute } from 'vue-router/auto';

const { t } = useI18n();
const route = useRoute();

route.meta.title = t('addServer');
</script>
