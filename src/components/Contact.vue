<script setup>
    import { ref, onMounted, onBeforeMount } from 'vue';

    import { Notyf } from 'notyf';
    import 'notyf/notyf.min.css';

    const notyf = new Notyf();

    const WEB3FORMS_ACCESS_KEY = "bd4311f2-ba27-480f-a205-da4cab6c4f19"

    const subject = "New message from Portfolio Contact Form";

    const name = ref("");
    const email = ref("");
    const message = ref("");

    const isLoading = ref(false);


    const submitForm = async() => {

        if(!recaptchaToken.value) {
            notyf.error('Please verify that you are not a robot.');
            return;
        }

        isLoading.value = true;

        try {

            const response = await fetch("https://api.web3forms.com/submit", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    Accept: "application/json"
                },
                body: JSON.stringify({
                    access_key: WEB3FORMS_ACCESS_KEY,
                    subject: subject,
                    name: name.value,
                    email: email.value,
                    message: message.value
                })
            });

            const result = await response.json();

            if(result.success) {
                console.log(result)

                isLoading.value = false;
                notyf.success("Message sent!");
            }

        } catch(error) {
            console.log(error);

            isLoading.value = false;
            notyf.error("Failed to send message");
        } finally {

            resetRecaptcha();
        }
    }

    /*recaptcha integration*/

    const SITE_KEY = '6LcpMvUsAAAAAE2z6OEh7jMZe_Yo3zp1ieU1VxhJ';

    const recaptchaContainer = ref(null);
    const recaptchaWidgetId = ref(null);
    const recaptchaToken = ref('');


    function onRecaptchaSuccess(token) {
        recaptchaToken.value = token;
    }

    function onRecaptchaExpired() {
        recaptchaToken.value = '';
    }

    function renderRecaptcha() {
        if(!window.grecaptcha) {
            console.error('reCAPTCHA not loaded');
            return;
        }

        recaptchaWidgetId.value = window.grecaptcha.render(recaptchaContainer.value, {
            sitekey: SITE_KEY,
            size: 'normal',
            callback: onRecaptchaSuccess,
            'expired-callback': onRecaptchaExpired
        });
    }

    function resetRecaptcha() {
        if(recaptchaWidgetId.value !== null) {
            window.grecaptcha.reset(recaptchaWidgetId.value);
            recaptchaToken.value = '';
        }
    }

    onMounted(() => {
        const interval = setInterval(() => {
            if(window.grecaptcha && window.grecaptcha.render) {
                renderRecaptcha();
                clearInterval(interval)
            }
        }, 100);

        onBeforeMount(() => {
            clearInterval(interval);
        });
    })
</script>

<template>
    <section class="contact-section p-4 p-md-5 py-5 mb-5" id="contact">
        <div class="contact-bg-icon">
            <span class="material-symbols-outlined">mail</span>
        </div>
        <form id="contact-form">
            <h2 class="contact-text-1 section-title ink-bleed mb-3">
                Let's start a conversation
            </h2>
            <p class="contact-text-2 mb-5">
                If you like my work and want to be in touch, my inbox is always open.
            </p>
            <div class="mb-4">
                <div class="row g-4 mb-4">
                    <div class="col-12 col-md-6">
                        <label for="name" class="contact-label">Name</label>
                        <input v-model="name" id="name" class="contact-input" placeholder="Your name here..." type="text" />
                    </div>
                    <div class="col-12 col-md-6">
                        <label for="email" class="contact-label">Email</label>
                        <input v-model="email" id="email" class="contact-input" placeholder="your@email.com" type="email" />
                    </div>
                </div>
                <div class="mb-4">
                    <label for="message" class="contact-label">Message</label>
                    <textarea v-model="message" id="message" class="contact-input" rows="4"></textarea>
                </div>
                <button class="btn-primary-custom" type="submit" onclick="location.href='#landing'">
                    {{isLoading ? "Sending..." : "Send Message"}}
                    <span class="material-symbols-outlined">send</span>
                </button>
            </div>
            <div class="d-flex justify-content-end mt-2">
                <div ref="recaptchaContainer"></div>
            </div>
        </form>
    </section>
</template>