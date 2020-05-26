<template>
    <button :class="{[`icon-${iconPosition}`]:true}" class="g-button">
        <svg aria-hidden="true" v-if="icon">
            <use :xlink:href=`#i-${icon}`></use>
        </svg>
        <span class="text"><slot></slot></span>
    </button>
</template>

<script>
    export default {
        // props:['icon','iconPosition']
        props: {
            icon: {},
            iconPosition: {
                type: String,
                default: 'left',
                validator: function (value) {
                    console.log(value)
                    if (value != 'left' && value != 'right') {
                        return true
                    } else {
                        return false
                    }
                }
            }
        }
    }

</script>

<style lang="scss">
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

        &:hover {
            border-color: var(--border-color-hover);
        }

        &:active {
            background-color: var(--button-active-bg);
        }

        &:focus {
            outline: none;
        }

        > svg {
            order: 1;
            margin-right: .3em;
        }

        > .text {
            order: 2;
        }

        &.icon-right {
            > svg {
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