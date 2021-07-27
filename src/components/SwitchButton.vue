<template>
<div v-on:click="toggle" class="select-none cursor-pointer inline-block">
    <input type="checkbox" :name="name" v-model="isEnabled" class="hidden">
    <div class="rounded-full w-12 p-1 flex" :class="{'justify-end bg-gray-700 ': isEnabled, 'bg-gray-100 shadow-inner': !isEnabled}">
        <div class="w-5 h-5 rounded-full" :class="{'bg-gray-100': isEnabled, 'bg-white border': !isEnabled}">&nbsp;</div>
    </div>
</div>
</template>

<script>
export default {
    props: [
        'value',
        'name',
    ],
    data () {
        return {
            isEnabled: this.value
        }
    },
    model: {
        prop: 'value',
        event: 'change'
    },
    watch: {
        value: function() {
            this.isEnabled = this.value;
        }
    },
    methods: {
        toggle () {
            this.isEnabled = !this.isEnabled
            this.$emit('change', this.isEnabled)
        }
    }
}
</script>
