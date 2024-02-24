<template>
  <div>
    <div class="splashBackground">
      <div class="splashLogo" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, unref, onMounted } from 'vue';
import { useI18n } from 'vue-i18n';
import { useRouter } from 'vue-router/auto';
import { remote } from '@/plugins/remote';

const router = useRouter();
const i18n = useI18n();
const valid = ref(false);
const previousServerLength = unref(remote.auth.servers.length);
const serverUrl = ref('https://www.mzxt.in'); // Changed to a ref
const loading = ref(false);

const rules = [
  (v: string): boolean | string => !!v.trim() || i18n.t('required')
];

/**
 * Attempts a connection to the given server
 */
async function connectToServer(): Promise<void> {
  loading.value = true;

  try {
    await remote.auth.connectServer(serverUrl.value); // Accessing value from ref

    await (previousServerLength === 0
      ? router.push('/server/login')
      : router.push('/server/select'));
  } finally {
    loading.value = false;
  }
}

onMounted(connectToServer); // Call connectToServer when component is mounted
</script>
