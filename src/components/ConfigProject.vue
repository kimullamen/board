<template>
  <v-card>
    <v-card-title @click="show = !show">
      プロジェクト名 の編集
    </v-card-title>
    <v-card-text v-show="show">
      <v-form v-model="valid" ref="form" lazy-validation @submit.prevent="submit">
        <v-layout row wrap>
          <v-flex>
            <v-text-field
            :label="'プロジェクト名'"
            v-model="project.name"
            :rules="nameRules"
            required
            ></v-text-field>
          </v-flex>
        </v-layout>
        <v-btn type="submit" color="primary">save</v-btn>
      </v-form>
    </v-card-text>
  </v-card>
</template>

<script>

export default {
  name: 'ConfigProject',
  data () {
    return {
      valid: false,
      project: {
        name: null
      },
      nameRules: [
        (v) => /^[a-zA-Z0-9_-]+$/.test(v) || '半角英数字で入力してください'
      ],
      show: false
    }
  },
  methods: {
    submit: function () {
      if (this.$refs.form.validate()) {
        this.$store.commit('updateProject', this.project)
        this.show = !this.show
      }
    }
  },
  created () {
    this.project = JSON.parse(JSON.stringify(this.$store.state.project))
  }
}
</script>
