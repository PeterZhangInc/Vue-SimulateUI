<template>
    <div class="su-number">
        <div class="su-number__btn simulate-ui su-minus" @click="minus"></div>
        <div class="su-number__input su-number__input__readonly">
            {{ current }}
        </div>
        <div class="su-number__btn  simulate-ui su-plus" :class="classes" @click="plus"></div>
    </div>
</template>
<script>
    import cx from 'classnames'
    export default{
        model: {
            prop: 'value',
            event: 'change'
        },
        props: {
            value: Number,
            min: Number,
            max: Number,
            step: {
                type: Number,
                default: 1
            },
            color: {
                type: String,
                default: 'primary'
            }
        },
        data(){
            return {
                current: 0
            }
        },
        computed: {
            classes() {
                return cx({
                    [`su-number__btn__${this.color}`]: true
                })
            }
        },
        methods: {
            plus() {
                const val = this.current + this.step
                if ( typeof this.max != 'undefined' && val > this.max ) {
                    this.current = this.max
                } else {
                    this.current += this.step
                }

                this.$emit('input', this.current)
                this.$emit('change', this.current)
            },
            minus() {
                const val = this.current - this.step
                if ( typeof this.min != 'undefined' && val < this.min) {
                    this.current = this.min
                } else {
                    this.current -= this.step
                }

                this.$emit('input', this.current)
                this.$emit('change', this.current)
            }
        }
    }
</script>
