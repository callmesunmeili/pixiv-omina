<template>
  <el-input
    v-model="value"
    disabled>
    <el-button
      slot="append"
      icon="el-icon-folder"
      @click="selectDirectory"
    ></el-button>
  </el-input>
</template>

<script>
import { ipcRenderer } from 'electron';

export default {
  props: {
    value: {
      required: true,
      type: String,
      default: ''
    }
  },

  methods: {
    selectDirectory() {
      let { filePath, bookmarks } = ipcRenderer.sendSync('setting-service', {
        action: 'selectDirectory',
        args: {}
      });

      this.$emit('input', filePath.length > 0 ? filePath[0] : this.value);
    }
  }
}
</script>
