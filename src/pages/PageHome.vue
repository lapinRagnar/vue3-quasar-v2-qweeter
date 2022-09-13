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
          @click="addNewQweet"
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


    <transition
      appear
      enter-active-class="animated fadeIn slower"
      leave-active-class="animated fadeOut slower"
    >

      <q-list>

        <q-item
          class="q-py-md"
          v-for="qweet in qweets" :key="qweet.date"
          >
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
              {{ qweet.content}}
            </q-item-label>

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
                @click="deleteQweet(qweet)"
                flat
                round
                color="grey"
                icon="fas fa-trash"
                size="sm"
              />

            </div>


          </q-item-section>
            {{ formaterDate(qweet.date) }}
          <q-item-section side top>

          </q-item-section>
        </q-item>

        <q-separator inset="item" />

      </q-list>


    </transition>




  </q-page>

</template>

<script>

import { defineComponent } from 'vue'
import { useTimeAgo } from '@vueuse/core'

export default defineComponent({
  name: 'PageHome',
  data(){
    return {
      newQweetContent: '',
      qweets: [
        {
          content: 'Lorem ipsum dolor sit, amet consectetur adipisicing elit. Maiores vitae laboriosam aut ipsa nostrum expedita totam ea quam corporis, quod, ad sunt amet aliquam, fuga itaque. Magni pariatur eum ea?',
          date: 1663055201593
        },
        {
          content: "Lorem Ipsum est un générateur de faux textes aléatoires. Vous choisissez le nombre de paragraphes, de mots ou de listes. Vous obtenez alors un texte aléatoire que vous pourrez ensuite utiliser librement dans vos maquettes.",
          date: 1663055445649
        },
      ],

    }
  },
  computed: {
    relativeDate(value) {
      return formatDistance(value, new Date())
    }
  },
  methods: {
    formaterDate(value){
      return useTimeAgo(value)
    },

    addNewQweet(){
      let newQweet = {
        content: this.newQweetContent,
        date: Date.now()
      }

      this.qweets.unshift(newQweet)
      this.newQweetContent = ''
    },

    deleteQweet(qweet){
      console.log(qweet)
      let qweetToDelete = qweet.date
      let index = this.qweets.findIndex(qweet => qweet.date == qweetToDelete)
      console.log(index);
      this.qweets.splice(index, 1)
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
