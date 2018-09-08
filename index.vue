<style scoped>
    .input-image {
        display: inline-block
    }
</style>

<template>
    <div class="input-image-webcam">

        <span class="button is-small" @click="active_take_pic_modal = true">
            <b-icon size="is-small" icon="camera" />
            <span>{{cta}}</span>
        </span>

        <b-modal :active.sync="active_take_pic_modal" has-modal-card>
            <vue-webcam ref='webcam' />
            <div class="has-text-centered">
                <button class="button is-success" @click="take_pic">
                    <span class="icon is-small">
                        <i class="fas fa-check"></i>
                    </span>
                    <span>{{$t('ready')}}</span>
                </button>
            </div>
        </b-modal>

    </div>
</template>

<script>

    import vueWebcam from 'vue-webcam'

    export default {

        name: 'input-img64',

        data () {
            return {
                active_take_pic_modal: false
            }
        },

        props: {
            size: {
                type: String,
                default: ''
            },
            cta: {
                type: String,
                default: 'Click to pick an image'
            }
        },

        methods: {
            take_pic () {
                const image = this.$refs.webcam.getPhoto()
                this.$emit('input', image)
                this.active_take_pic_modal = false
            }
        },

        components: {
            vueWebcam
        }
    }
</script>