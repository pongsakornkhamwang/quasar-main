<template>
  <div class="q-pa-md" style="max-width: 400px">

    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
      >
      <q-input
        filled
        v-model="language"
        label="ภาษา *"
        hint="ภาษา"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'กรุณาใส่ภาษา']"
      />
      <q-input
        filled
        v-model="id"
        label="Your id *"
        hint="id-code "
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type your id-code']"
        />
      <q-input
        filled
        v-model="name"
        label="name *"
        hint="Name "
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type something']"
      />
      <q-input
        filled
        v-model="surname"
        label="Your surname *"
        hint="surname "
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type something']"
      />

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
    const id = ref("6604101352")
    const name = ref("พงศกร")
    const surname = ref("คำวัง")
    const language = ref ("ภาษาไทย")
    const age = ref(null)
    const accept = ref(false)

    return {
      id,
      name,
      surname,
      age,
      accept,
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
        id.value =null
        surname.value = null
        name.value = null
        age.value = null
        accept.value = false
        language.value = null
      }
    }
  }
}
</script>
