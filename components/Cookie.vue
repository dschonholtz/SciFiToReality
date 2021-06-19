<template>
    <div v-show="isOpen"
         class="uk-alert">
        <div>
            <p>
                Can I use cookies for analytics? Read
                <nuxt-link to="/blog/PrivacyPolicy">the privacy policy</nuxt-link>
                for more information.
            </p>
            <div class="uk-button uk-button-default" @click="accept">Yes, sure</div>
            <div class="uk-button uk-button-default" @click="deny">Nah</div>
        </div>
    </div>
</template>


<script>
import {bootstrap} from 'vue-gtag';

  export default {
      
    data() {
        return {
            isOpen: false
        };
    },
    created() {
        if (!this.getGDPR() === true) {
            this.isOpen = true;
        }
    },
    methods: {
        accept() {
            if (process.browser) {
                bootstrap().then(gtag => {
                    this.isOpen = false;
                    localStorage.setItem('GDPR:accepted', true);
                    location.reload();
                })
            }
        },
        deny() {
            if (process.browser) {
                this.isOpen = false;
                localStorage.setItem('GDPR:accepted', false);
            }
        },
        getGDPR() {
            if (process.browser) {
                return localStorage.getItem('GDPR:accepted', true);
            }
        },
    }

  }
</script>

<style scoped lang="scss">
</style>