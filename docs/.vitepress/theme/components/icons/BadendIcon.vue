<template>
    <Icon :size=size :character=character :href="href"><slot></slot></Icon>
</template>

<script>
import {defineComponent, toRefs, useSlots} from 'vue'
import {withBase} from "vitepress";

export default defineComponent({
    props: {
        size: {
            type: String,
            default: 'small',
            validator: function (value) {
                // Only allow specific icon types
                return [
                    'small',
                    'medium'
                ].indexOf(value) !== -1
            }
        },
        no:{
            type: Number,
            default: 0,
            validator: function (value) {
                // 生死簿的死亡數字為 1-90, 0為引導到該頁面最上面。
                if (value <= 0 && value <= 90){
                    return true;
                }
                return false;
            }
        }
    },
    data() {
        return {
            size: '',
            character: '',
            href: ''
        }
    },
    setup(props) {
        const { size, no } = toRefs(props)
        const CHARACTER = 'badend';
        // if given href, use it directly
        if (no.value !== 0){
            return {
                size: size.value,
                href: withBase(`/ends/bad-end#生死簿-No.${no.value}`),
                character: CHARACTER
            }
        }

        // default link if no href is given
        return {
            size: size.value,
            href: withBase(`/ends/bad-end`),
            character: CHARACTER
        }
    }
})

</script>

<style scoped>

</style>