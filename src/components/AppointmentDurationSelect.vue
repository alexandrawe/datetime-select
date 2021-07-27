<template>
<div class="space-y-4">
    <div class="bg-white rounded p-6 space-y-2">
        <div class="flex justify-between items-center space-x-4">
            <div>Von:</div>
            <date-time-select v-model="fromDate" :allday-time="'00:00'" :is-allday="allday" @updatedDatetime="setFromDatetime"></date-time-select>
        </div>
        <div class="flex justify-between items-center space-x-4">
            <div>Bis:</div>
            <date-time-select :allday-time="'23:59'" :is-allday="allday" @updatedDatetime="setUntilDatetime"></date-time-select>
        </div>
        <div class="flex items-center">
            <switch-button :name="allday" :value="allday" v-model="allday"></switch-button>
            <span class="pl-2">ganztägig</span>
        </div>
    </div>

</div>
</template>

<script>
import SwitchButton from './SwitchButton.vue'
import DateTimeSelect from './DateTimeSelect.vue';

export default {
    data: function () {
        return {
            allday: false,
            fromDate: null,
            untilDate: null,
        }
    },
    components: {
        DateTimeSelect,
        SwitchButton,
    },
    methods: {
        setFromDatetime(datetime) {
            this.fromDate = datetime;
        },
        setUntilDatetime(datetime) {
            this.untilDate = datetime;
        },
    }
}
</script>