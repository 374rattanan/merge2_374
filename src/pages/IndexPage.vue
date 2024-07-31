<template>
  <div class="q-pa-md" style="max-width: 400px">

    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
    >
      <!-- id -->
      <q-input
        filled
        v-model="id"
        label="Your id*"
        hint="id-code"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type your id']"
      />
      <!-- name -->
      <q-input
        filled
        v-model="name"
        label="Your name *"
        hint="Name and surname"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type your name']"
      />
      <!-- surname -->
      <q-input
        filled
        v-model="surname"
        label="surname*"
        hint="surname"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type surname']"
      />
      <!-- Language -->
      <q-input
        filled
        v-model="language"
        label="ภาษา *"
        hint="ภาษา"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'กรุณาใส่ภาษา']"
      />     
      <!-- age -->
      <q-input
        filled
        type="number"
        v-model="age"
        label="Your age *"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || 'Please type your age',
          val => val > 0 && val < 100 || 'Please type a real age'
        ]"
      />

      <q-toggle v-model="accept" label="I accept the license and terms" />

      <div>
        <q-btn label="Submit" type="submit" color="primary"/>
        <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>

  </div>
</template>

<script>
import { useQuasar } from 'quasar'
import { ref } from 'vue'

export default {
  setup () {
    const $q = useQuasar()

    const name = ref("ชื่อ")
    const age = ref(null)
    const accept = ref(false)
    const surname = ref("นามสกุล")
    const id = ref("66.....")
    const language = ref("ภาษาไทย")

    return {
      name,
      age,
      accept,
      surname,
      id,
      language,

      onSubmit () {
        if (accept.value !== true) {
          $q.notify({
            color: 'red-5',
            textColor: 'white',
            icon: 'warning',
            message: 'You need to accept the license and terms first'
          })
        }
        else {
          $q.notify({
            color: 'green-4',
            textColor: 'white',
            icon: 'cloud_done',
            message: 'Submitted'
          })
        }
      },

      onReset () {
        name.value = null
        age.value = null
        accept.value = false
        surname.value=null
        id.value=null
      }
    }
  }
}
</script>
