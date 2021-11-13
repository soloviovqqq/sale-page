<template>
    <div class="container">
        <div class="row">
            <div class="col-md-6 offset-md-3 my-5">
                <div class="card">
                    <div class="card-body">
                        <img src="./assets/logo.png" class="img-fluid sale-poster">
                        <hr/>
                        <h2 class="mb-4 sale-header">Sale Option 1 Waiting Room</h2>
                        <p class="mb-4">Sale Option 1 has not yet started.</p>
                        <p class="mb-4">When it starts at 5:00 PM UTC, you will be assigned a random place in line alongside everyone else who arrived in this waiting room before the start and in front of those who arrive after the start.</p>
                        <hr>
                        <p class="text-center my-4"><b>The event will began at: 5:00 PM UTC</b></p>

                        <div class="sale-timer d-flex align-items-center flex-column" v-if="timerCount > 29">
                            <div class="mb-auto p-2"><h1>30 Minutes {{ timerCount }} Seconds</h1></div>
                            <img src="https://www.nicepng.com/png/full/244-2444375_rhodes-online-green-dot-icon.png" width="15">
                            <div class="p-2 bd-highlight">Status last updated: 1:02:03 PM</div>
                        </div>

                        <div class="text-center mt-4" v-else>
                            <button type="button"
                                    class="btn btn-primary btn-lg"
                                    @click="showCaptcha"
                                    v-if="!captchaShowing">
                                Re-enter the waiting room
                            </button>
                            <vue-recaptcha v-else
                                           sitekey="6LdGLjEdAAAAAAnbzxUm8LsjM2eviACkT03fN_I0"
                                           @verify="captchaVerified"/>

                            <h2 v-if="captchaComplited">🥳🥳 Captcha complited successfully🎉🎉</h2>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import VueRecaptcha from 'vue-recaptcha';

    export default {
        components: {
            VueRecaptcha
        },
        data() {
            return {
                timerCount: 40,
                captchaShowing: false,
                captchaComplited: false,
            }
        },
        watch: {
            timerCount: {
                handler(value) {
                    if (value > 0) {
                        setTimeout(() => {
                            this.timerCount--;
                        }, 1000);
                    }
                },
                immediate: true,
            }
        },
        methods: {
            showCaptcha() {
                this.captchaShowing = true;
            },
            captchaVerified() {
                this.captchaComplited = true;
            }
        }
    }
</script>

<style>
    body {
        background: #f6f6f7;
    }

    .sale-header {
        color: #e83892;
    }

    .btn {
        box-shadow: none !important;
        background: #e83892;
        border-color: #a7286a;
    }

    .btn:hover, .btn:active {
        background: #f24ba0 !important;
        border-color: #f24ba0 !important;
    }

    .sale-poster {
        border-radius: 1em;
    }

    .sale-timer {
        padding: 30px;
        height: 250px;
        border-radius: 0.5em;
        background: #dbdbdb;
    }
</style>
