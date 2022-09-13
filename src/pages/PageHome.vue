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

    <q-separator class="divider" size="10px" color="grey-2" />


    <!-- liste de qweet -->

    <q-list>

      <q-item class="q-py-md">
        <q-item-section avatar>
          <q-avatar>
            <img src="https://cdn.quasar.dev/img/avatar2.jpg">
          </q-avatar>
        </q-item-section>

        <q-item-section>

          <q-item-label>
            <strong>lapinragnar</strong>
            <span class="text-grey-7">
              @lapinragnar
            </span>
          </q-item-label>
          <q-item-label class="qweet-content">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Quis facere alias,
            necessitatibus magni maxime, rem vero, veniam eum enim vel molestiae.
            
            Ratione commodi doloremque obcaecati culpa quasi praesentium esse dolores.
          </q-item-label>
        </q-item-section>

        <q-item-section side top>
          1 min ago
        </q-item-section>
      </q-item>

      <q-separator inset="item" />

    </q-list>


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

  .divider{
    border-top: 1px solid;
    border-bottom: 1px solid;
    border-color: $orange-2;
  }

  .qweet-content{
    white-space: pre-line;
  }
</style>
