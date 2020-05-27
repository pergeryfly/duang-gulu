<template>
    <button :class="{[`icon-${iconPosition}`]:true}" @click="$emit('click')" class="g-button">
        <g-icon :name="icon" class="icon" v-if="icon&&!loading"></g-icon>
        <g-icon class="loading icon" name="loading" v-if="loading"></g-icon>
        <span class="text"><slot></slot></span>
    </button>
</template>

<script>
    export default {
        // props:['icon','iconPosition']
        props: {
            icon: {},
            loading: {
                type: Boolean,
                default: false,
            },
            iconPosition: {
                type: String,
                default: 'left',
                validator: function (value) {
                    if (!(value != 'left' && value != 'right')) {
                        return false
                    } else {
                        return true
                    }
                }
            }
        }
    }

</script>

<style lang="scss">
    @keyframes spin {
        0% {
            transform: rotate(0deg);
        }
        100% {
            transform: rotate(360deg)
        }
    }

    .g-button {
        height: var(--button-height);
        padding: 0 1em;
        border-radius: var(--border-radius);
        border: 1px solid var(--border-color);
        background: var(--button-bg);
        display: inline-flex;
        justify-content: center;
        align-items: center;
        vertical-align: top;

        .loading {
            animation: spin 1s infinite linear;
        }

        &:hover {
            border-color: var(--border-color-hover);
        }

        &:active {
            background-color: var(--button-active-bg);
        }

        &:focus {
            outline: none;
        }

        > .icon {
            order: 1;
            margin-right: .3em;
        }

        > .text {
            order: 2;
        }

        &.icon-right {
            > .icon {
                order: 2;
                margin-right: 0;
                margin-left: .3em;
            }

            > .text {
                order: 1;
            }
        }
    }


</style>