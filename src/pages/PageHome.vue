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
        <q-item-section avatar top>
          <q-avatar>
            <img src="https://cdn.quasar.dev/img/avatar2.jpg">
          </q-avatar>
        </q-item-section>

        <q-item-section>

          <q-item-label class="text-subtitle1">
            <strong>lapinragnar</strong>
            <span class="text-grey-7">
              @lapinragnar
            </span>
          </q-item-label>

          <q-item-label class="qweet-content text-body1 q-pt-lg">

            <p>

              Lorem ipsum dolor sit amet consectetur adipisicing elit. Quis facere alias,
              necessitatibus magni maxime, rem vero, veniam eum enim vel molestiae.

              Ratione commodi doloremque obcaecati culpa quasi praesentium esse dolores.

              Lorem ipsum dolor sit, amet consectetur adipisicing elit. Maiores vitae laboriosam aut ipsa nostrum expedita totam ea quam corporis, quod, ad sunt amet aliquam, fuga itaque. Magni pariatur eum ea?


            </p>

            <div class="row justify-between q-mt-sm">

              <q-btn
                flat
                round
                color="grey"
                icon="far fa-comment"
                size="sm"
              />

              <q-btn
                flat
                round
                color="grey"
                icon="fas fa-retweet"
                size="sm"
              />

              <q-btn
                flat
                round
                color="grey"
                icon="far fa-heart"
                size="sm"
              />
              <q-btn
                flat
                round
                color="grey"
                icon="fas fa-trash"
                size="sm"
              />

            </div>

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
    p{
      white-space: pre-line !important ;
    }
  }
</style>
