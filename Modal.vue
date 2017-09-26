<template>
    <transition name="modal">
        <div>
            <div :class="'modal ' + modalClasses" tabindex="-1" role="dialog" aria-labelledby="Modal" style="display: block" @click.stop="closeBackdrop">
                <div :class="'modal-dialog ' + modalSizeClasses" role="document" @click.stop="">
                    <div class="modal-content">

                        <div class="modal-header" v-if="hasHeader">
                            <h5 class="modal-title">{{ title }}</h5>

                            <button type="button" class="close" aria-label="Close" @click="close">
                                <span aria-hidden="true">&times;</span>
                            </button>
                        </div>

                        <slot></slot>
                    </div>
                </div>
            </div>

            <div class="modal-backdrop show"></div>
        </div>
    </transition>
</template>

<style lang="scss" scoped>
    .modal {
        overflow-x: hidden;
        overflow-y: auto;
    }

    button.close {
        cursor: pointer;
    }

    /* Transitions */
    .modal-enter-active, .modal-leave-active {
        transition: opacity .3s linear;
    }

    .modal-enter-active .modal, .modal-leave-active .modal,
    .modal-enter-active .modal-backdrop, .modal-leave-active .modal-backdrop {
        transition: opacity .15s linear;
    }

    .modal-enter .modal, .modal-leave-to .modal, .modal-leave-active .modal,
    .modal-enter .modal-backdrop, .modal-leave-to .modal-backdrop, .modal-leave-active .modal-backdrop {
        opacity: 0
    }

    .modal-enter-active .modal-dialog, .modal-leave-active .modal-dialog {
        transition: transform .3s ease-out;
    }

    .modal-enter .modal-dialog, .modal-leave-to .modal-dialog, .modal-leave-active .modal-dialog {
        transform: translate(0, -25%);
    }
</style>

<script type="text/babel">
    export default {
        props: {
            "title": {default: ""},

            "modalClasses": {default: ""},

            "isLarge": {default: false},
            "isSmall": {default: false},

            "hasHeader": {default: true},

            "backdropClose": {default: true},
            "backdropCloseConfirm": {default: false},
            "backdropCloseConfirmText": {default: "Are you sure?"},
        },

        data() {
            return {}
        },

        methods: {
            close() {
                this.$emit("close");
            },

            closeBackdrop() {
                if (!this.backdropClose) {
                    return false;
                }

                if (this.backdropCloseConfirm && !confirm(this.backdropCloseConfirmText)) {
                    return false;
                }

                this.close();
            }
        },

        computed: {
            modalSizeClasses() {
                if (this.isLarge) {
                    return "modal-lg";
                }

                if (this.isSmall) {
                    return "modal-sm";
                }

                return "";
            }
        },

        mounted() {
        },

        destroyed() {
        }
    }
</script>
