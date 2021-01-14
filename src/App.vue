<template>
  <div class="wrapper">
    <div class="wrapper-content">

      <section>
        <div class="container">

          <!-- first modal -->
          <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Show first modal</button>
          <modals
            title="First modal"
            v-show="modalFirst"
            @close="modalFirst = false">
            <!-- body -->
            <div slot="body">
              <p style="margin-bottom: 20px"> Text  </p>
              <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Well Done!</button>
            </div>
          </modals>

          <!-- Second modal -->
          <button class="btn btnPrimary" @click="modalSecond.show = !modalSecond.show ">Show  modal width form</button>
          <modals
            title="Modal width form"
            v-show="modalSecond.show"
            @close="modalSecond.show= false">
            <!-- body -->
            <div slot="body">
             <form @submit.prevent="SubmitSecondForm">
               <label >Name:</label>
               <input type="text" v-model="modalSecond.name" required>
               <label >Email:</label>
               <input type="email" v-model="modalSecond.email" required>
              <button class="btn btnPrimary" >Submit</button>
              </form>
            </div>
          </modals>
          <!-- modal with validate -->
          <button class="btn btnPrimary" @click="modalValidate = !modalValidate ">Show  modal width form + validate</button>
          <modalValidate v-show="modalValidate" @close="modalValidate= false"></modalValidate>

        </div>
      </section>


    </div>
  </div>
</template>

<script>
import modals from '@/components/UI/Modal.vue'
import modalValidate from '@/components/ModalValidate.vue'

export default {
  components: { modals,modalValidate },
  data () {
    return {
      modalFirst: false,
      modalSecond: {
        show: false,
        name: '',
        email: ''
      },
      modalValidate: false
    }
  },
  methods: {
    SubmitSecondForm () {
      console.log({
        name: this.modalSecond.name,
        email: this.modalSecond.email
      })
      this.modalSecond.name = '',
      this.modalSecond.email = ''
      this.modalSecond.show = false
    }
  }
}
</script>
