<template>
    <modal
            title="Modal width form"
            @close="$emit('close')">
            <!-- body -->
            <div slot="body">
             <form @submit.prevent="onSubmit">
               <!-- name -->
               <div class="form-item" :class="{errorInput: $v.name.$error}">
               <label >Name:</label>
               <p class="error-text" v-if="!$v.name.required">Filed is required!</p>
               <p class="error-text" v-if="!$v.name.minLength">Name must have at least {{$v.name.$params.minLength.min}}!</p>
               <input type="text" 
               v-model="name"
               :class="{error:  $v.name.$error}"
               @change="$v.name.$touch()">
               </div>
              <!-- email -->
                <div class="form-item" :class="{errorInput: $v.email.$error}">
               <label >Email:</label>
               <p class="error-text" v-if="!$v.email.required">Filed is required!</p>
               <p class="error-text" v-if="!$v.email.email">Email is not correct!</p>
               <input type="email" 
               v-model="email"
               :class="{error:  $v.email.$error}"
               @change="$v.email.$touch()">
               </div>
              <button class="btn btnPrimary" >Submit</button>
              </form>
            </div>
          </modal>
</template>

<script>
import { required, minLength, email} from 'vuelidate/lib/validators'
import modal from '@/components/UI/Modal.vue'
export default {
    components: {modal},
    data() {
    return {
      name: '',
      email: ''
    }
  },
  validations: {
    name: {
      required,
      minLength: minLength(4)
    },
    email: {
       required,
       email
    }
  },
  methods: {
    onSubmit () {
      this.$v.$touch()
      if(!this.$v.$invalid) {
        const user = {
          name: this.name,
          email: this.email
        }
        console.log(user)
        this.name = '',
        this.email = '',
        this.$v.$reset()
        this.$emit('close')
      }
    }
  }
}
</script>
<style lang="scss" >
.form-item .error-text{
  display: none;
  margin-bottom: 8px;
  font-size: 13px;
  color: rgb(236, 9, 9);
}
.form-item {
  &.errorInput .error-text{
    display: block;

  }
}
input.error{
  border-color:rgb(236, 9, 9);
}

</style>