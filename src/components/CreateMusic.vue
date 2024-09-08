<template>
  <v-sheet class="mx-auto" width="300">
    <v-form fast-fail :key="formKey" ref="form" @submit.prevent="saveMusic">
      <v-text-field
        v-model="music.name"
        :rules="stringRules"
        label="Nome da música"
      ></v-text-field>

      <v-text-field
        v-model="music.style"
        :rules="stringRules"
        label="Estilo musical"
      ></v-text-field>

      <v-select
        v-model="music.score"
        :items="items"
        label="Pontuação"
      ></v-select>

      <v-btn class="mt-2" type="submit" block>Cadastrar</v-btn>
    </v-form>
  </v-sheet>

  <v-table>
    <thead>
      <tr>
        <th class="text-left">
          Nome da música
        </th>
        <th class="text-left">
          Estilo Musical
        </th>
        <th class="text-left">
          Pontuação
        </th>
      </tr>
    </thead>
    <tbody>
      <tr
        v-for="item in musics"
        :key="item.name"
      >
        <td>{{ item.name }}</td>
        <td>{{ item.style }}</td>
        <td>{{ item.score }}</td>
      </tr>
    </tbody>
  </v-table>
</template>

<script>
  export default {
    data: () => ({
      musics: [],
      music: {name: '', style: '', score: null},
      stringRules: [
        value => {
          if (value?.length >= 3) return true

          return 'First name must be at least 3 characters.'
        },
      ],
      items: [
        '1',
        '2',
        '3',
        '4',
        '5'
      ],
    }),
    methods: {
      saveMusic() {
          this.musics.push({ ...this.music })
          this.formKey++
          this.$refs.form.reset()
          this.$refs.form.resetValidation()
        }
    },
  }
</script>