<template>
<div class="space-y-4">
    <div class="flex space-x-4">
        <date-picker v-model="selectedDate" :type="'date'" :format="'D. MMMM YYYY'" :value-type="'YYYY-MM-DD'" :input-class="'rounded bg-gray-100 w-full px-2 py-0.5'" @close="updateDate"></date-picker>
        <date-picker v-if="!isAllday" v-model="selectedTime" :type="'time'" :format="'HH:mm'" :value-type="'HH:mm'" :minute-step="5" :input-class="'rounded bg-gray-100 w-full px-2 py-0.5'" @close="updateDate"></date-picker>
    </div>
</div>
</template>

<script>
import dayjs from 'dayjs'
import DatePicker from 'vue2-datepicker';

import 'vue2-datepicker/locale/de';
import 'vue2-datepicker/index.css';

export default {
    data: function () {
        return {
            selectedDate: null,
            selectedTime: null,
        }
    },
    props: {
        isAllday: {
            type: Boolean,
            required: false,
            default: false,
        },
        alldayTime: {
            type: String,
            required: false,
        },
        existingTimestamp: {
            type: String,
            required: false,
            default: null,
        },
    },
    components: {
        DatePicker,
    },
    computed: {
        datetime() {
            if(!this.selectedDate) return null;
            let time = this.isAllday ? this.alldayTime : this.selectedTime;
            return dayjs(this.selectedDate + 'T' + time).toISOString();
        },
    },
    watch: {
        isAllday(value) {
            if(value) {
                this.updateDate(this.datetime);
            }
        }
    },
    mounted() {
        this.setPrefilledDateAndTime();
        this.updateDate(this.datetime);
    },
    methods: {
        updateDate() {
            this.$emit('updatedDatetime', this.datetime)
        },
        setPrefilledDateAndTime() {
            if(this.existingTimestamp) {
                this.selectedDate = dayjs(this.existingTimestamp).format('YYYY-MM-DD');
                this.selectedTime = dayjs(this.existingTimestamp).format('HH:mm')
            }
        }
    },
}
</script>