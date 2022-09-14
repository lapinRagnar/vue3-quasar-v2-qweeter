<template>

  <q-page class="position-relative">

    <q-scroll-area class="absolute fullscreen">


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
            v-for="qweet in qweets"
            :key="qweet.id"
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
                  &bull; <br class="lt-md"> {{ formaterDate(qweet.date) }}
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

          </q-item>

          <q-separator inset="item" />

        </q-list>


      </transition>

    </q-scroll-area>

  </q-page>

</template>

<script>

import db from 'src/boot/firebase'
import { collection, query, onSnapshot, orderBy, addDoc, deleteDoc, doc } from "firebase/firestore";

import { defineComponent } from 'vue'
import { useTimeAgo } from '@vueuse/core'

export default defineComponent({
  name: 'PageHome',
  data(){
    return {
      newQweetContent: '',
      // qweets: [
      //   {
      //     content: 'Lorem ipsum dolor sit, amet consectetur adipisicing elit. Maiores vitae laboriosam aut ipsa nostrum expedita totam ea quam corporis, quod, ad sunt amet aliquam, fuga itaque. Magni pariatur eum ea?',
      //     date: 1663055201593
      //   },
      //   {
      //     content: "Lorem Ipsum est un générateur de faux textes aléatoires. Vous choisissez le nombre de paragraphes, de mots ou de listes. Vous obtenez alors un texte aléatoire que vous pourrez ensuite utiliser librement dans vos maquettes.",
      //     date: 1663055445649
      //   },
      // ],
      qweets: []

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

    async addNewQweet(){
      let newQweet = {
        content: this.newQweetContent,
        date: Date.now()
      }

      // this.qweets.unshift(newQweet)

      // Add a new document with a generated id.
      await addDoc(collection(db, "qweets"), newQweet)
        .then(docRef => {

          console.log("Document written with ID: ", docRef.id)
        })
        .catch(error => console.log('misy erreur ooooh', error))


      this.newQweetContent = ''
    },

    async deleteQweet(qweet){
      // console.log(qweet)
      // let qweetToDelete = qweet.date
      // let index = this.qweets.findIndex(qweet => qweet.date == qweetToDelete)
      // console.log(index);
      // this.qweets.splice(index, 1)

      console.log('id du qweet à supprimer',qweet.id)

      // await deleteDoc(doc(db, "qweet", qweet.id))
      //   .then(() => console.log('le qweet a bien été supprimé!'))
      //   .catch(error => console.log(error))

      const docRef = doc(db, "qweets", qweet.id)

      deleteDoc(docRef)
      .then(() => {
          console.log("Entire Document has been deleted successfully.")
      })
      .catch(error => {
          console.log(error)
      })


    }


  },
  mounted(){


    console.log('salut')
    console.log(db)



    const q = query(collection(db, "qweets"), orderBy("date", "asc"))

    onSnapshot(q, (snapshot) => {

      snapshot.docChanges().forEach((change) => {

        let qweetChange = change.doc.data()

        qweetChange.id = change.doc.id


        if (change.type === "added") {
          console.log("New qweets: ", qweetChange);
          this.qweets.unshift(qweetChange)
        }
        if (change.type === "modified") {
          console.log("Modified qweets: ", qweetChange);
        }
        if (change.type === "removed") {
          console.log("Removed qweets: ", qweetChange);
          let index = this.qweets.findIndex(qweet => qweet.id = qweetChange.id)
          this.qweets.splice(index, 1)
        }
      });
    });


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
