<template>
  <v-row align="start" class="row--35">
    <v-col lg="12" md="12" sm="12" cols="12" order="1" order-md="1" class="mt-10">
      <div class="section-title text-left mb--50 mb_sm--30 mb_md--30">
        <h2 class="heading-title">Schedule a meeting</h2>
        <p class="description">
          I work in EST timezone.
        </p>

        <a
          target="_self"
          :href="CONSTS.MAIN.basic.calendlyLink"
          class="rn-button-style--2 btn_solid"
          type="submit"
          value="submit"
        >
          Schedule
        </a>
      </div>
    </v-col>
    <v-col lg="12" md="12" sm="12" cols="12" order="2" order-md="2">
      <div class="section-title text-left mb--50 mb_sm--30 mb_md--30">
        <h2 class="heading-title">or Contact Me.</h2>
        <p class="description">
          I will reach back as soon as I get the request. Alternatively, feel free to contact me directly at 
  <a href="mailto:goldjin354@gmail.com">goldjin354@gmail.com</a> or by phone at 
  <a href="tel:+16092414413">+1 (609) 241-4413</a>.
        </p>
      </div>
      <div class="form-wrapper">
        <ValidationObserver v-slot="{ handleSubmit }">
          <form @submit.prevent="handleSubmit(onSubmit)">
            <ValidationProvider
              name="name"
              rules="required"
              v-slot="{ errors }"
            >
              <label>
                <input
                  type="text"
                  v-model="formData.name"
                  placeholder="Your Name *"
                />
                <span class="inpur-error">{{ errors[0] }}</span>
              </label>
            </ValidationProvider>

            <ValidationProvider
              name="email"
              rules="required|email"
              v-slot="{ errors }"
            >
              <label>
                <input
                  type="text"
                  rules="required|email"
                  v-model="formData.email"
                  placeholder="Your email *"
                />
                <span class="inpur-error">{{ errors[0] }}</span>
              </label>
            </ValidationProvider>

            <ValidationProvider
              name="subject"
              rules="required"
              v-slot="{ errors }"
            >
              <label>
                <input
                  type="text"
                  v-model="formData.subject"
                  placeholder="Write a Subject"
                />
                <span class="inpur-error">{{ errors[0] }}</span>
              </label>
            </ValidationProvider>

            <ValidationProvider
              name="message"
              rules="required"
              v-slot="{ errors }"
            >
              <label>
                <textarea
                  v-model="formData.message"
                  placeholder="Your Message"
                ></textarea>
                <span class="inpur-error">{{ errors[0] }}</span>
              </label>
            </ValidationProvider>

            <button
              class="rn-button-style--2 btn_solid"
              type="submit"
              value="submit"
              :disabled="!isSubmittable"
            >
              {{ formData.submit}}
            </button>
          </form>
        </ValidationObserver>
      </div>
    </v-col>
    <!-- <v-col lg="6" md="6" sm="12" cols="12" order="1" order-md="2">
      <div class="thumbnail mb_md--40 mb_sm--40">
        <div class="section-title text-left mb--50 mb_sm--30 mb_md--30">
          <p class="description">
            I will reach back as soon as I get the request.
          </p>
        </div>
      </div>
    </v-col> -->
  </v-row>
</template>

<script>
  import emailjs from '@emailjs/browser';
  import { ValidationObserver } from "vee-validate";
  import { ValidationProvider } from "vee-validate/dist/vee-validate.full.esm";

  export default {
    components: {
      ValidationObserver,
      ValidationProvider,
    },
    data() {
      return {
        formData: {
          name: "",
          email: "",
          subject: "",
          message: "",
          submit: 'Submit',
        },
        isSubmittable: true,
      };
    },
    methods: {
      onSubmit() {
        emailjs.send('service_cv04q6q', 'template_jmhacxx', {
          from_name: this.formData.name,
          from_email: this.formData.email,
          subject: this.formData.subject,
          message: this.formData.message,
        }, 'QpTnpP14gPrcZrE-S')
          .then((result) => {
            this.formData.submit = 'submitted'
            this.isSubmittable = false
          }, (error) => {
            this.formData.submit = 'submitted'
            this.isSubmittable = false
          });
      },
    },
  };
</script>
