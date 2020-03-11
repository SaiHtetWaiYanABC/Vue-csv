<template>
    <a :download="downloadName" :href="downloadUrl" :disabled="this.data.length === 0">
        <slot>
            <i class="fa fa-file-excel-o" aria-hidden="true"></i>
        </slot>
    </a>
</template>

<script>
import json2csv from 'json2csv';
export default {
    props: {
        fields: undefined,
        data: undefined,
        meta: [
            [
                {
                    'key': 'charset',
                    'value': 'utf-8'
                }
            ]
        ],
        downloadName: {
            default: 'order.csv'
        }
    },
    computed: {
        downloadUrl() {
            return this.data.length > 0 ? "data:text/csv; charset=utf-8," + encodeURIComponent(json2csv({data: this.data, fields: this.fields , meta: this.meta})) : 'javascript:void(0);';
        }
    }
}
</script>
