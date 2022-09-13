<template>

  <q-page>

    <div class="q-py-lg q-px-md row items-end q-col-gutter-md">

      <div class="col">

        <q-input
          class="new-qweet"
          bottom-slots
          v-model="newQweetContent"
          label="quoi de neuf docteur..."
          counter
          maxlength="280"
          placeholder="qu'est ce que tu raconte de beau..."
          autogrow
        >

          <template v-slot:before>
            <q-avatar size="xl">
              <img src="https://cdn.quasar.dev/img/avatar5.jpg">
            </q-avatar>
          </template>


        </q-input>


      </div>


      <div class="col col-shrink">

        <q-btn
          class="q-mb-lg"
          unelevated
          rounded
          color="primary"
          label="Qweet"
          no-caps
          :disable="!newQweetContent"
        />


      </div>




    </div>


  </q-page>

</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'PageHome',
  data(){
    return {
      newQweetContent: ''
    }
  }
})
</script>

<style lang="scss">
  .new-qweet{
    font-size: 19px;
  }
</style>
