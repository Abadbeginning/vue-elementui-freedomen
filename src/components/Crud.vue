<template>
<div>
    <fd-region
        @event="dddd"
        :columns="[ 
            {type: 'button-primary', value: 'pre', prop: 'pre'},
            {type: 'button-primary', value: 'next'},
        ]"
    >
     
    </fd-region>
    <fd-search 
        :columns="[
            {type: 'input', prop: 'input'},
            {type: 'button', prop: 'search', value: 'search'}
        ]"
        @event="event"
    />  
    <fd-search 
        :columns="[
            {type: 'input', prop: 'input'},
            {type: 'button', prop: 'search', value: 'search'}
        ]"
        @event="event"
    /> 
    <fd-search 
        :columns="[
            {type: 'input', prop: 'input'},
            {type: 'button', prop: 'search', value: 'search'}
        ]"
        @event="event"
    /> 
</div>
</template>

<script>   
    import freedomen from '../plug'
    const {search} = freedomen.action
	export default {
        label: '介绍',
        components: { 
        },
        computed: {
            cls () {
                let columns = []
                for (let i = 0; i < 100; i ++) {
                    columns.push({
                        type: 'input',
                        prop: 'p' + i,
                        placeholder: 'pleaceh',
                        style: {width: '220px'}
                    }) 
                }
                return columns
            }
        },
		data() {
			return { 
                formData: {text: '1'},
                codeCompxPlus: {cx: {cxDateStart: new Date()}, hytj: {}, mj: [{}], gg: {}, propList: [], prop: {}},
			}
        },
		methods: {
            button() {
                this.formData = {text: null}
            },
            calcMultiplyData(arr) {
                let res = [], cur = {}
                function search(deep = 0) {
                    if (deep >= arr.length) {
                        res.push(cur)
                        cur = Object.assign({}, cur)
                        return
                    }
                    for (let obj of arr[deep]) {
                        cur[obj.prop] = obj.value
                        search(deep + 1)
                    }
                }
                search()
                return res
            },
            codeCompxPlusEvent(params) {
                if (params.prop == 'province') {
                    this.codeCompxPlus.city = ''
                     this.codeCompxPlus.area = ''
                } else if (params.prop == 'city') {
                    this.codeCompxPlus.area = ''
                } else if (params.prop == 'type') {
                    this.codeCompxPlus.propList = []
                }
            },
            dddd(params) {
                if (params.prop == 'pre') {
                    search.doAction({
                        prop: 'search'
                    })
                }
            },
            event(params) {
                if (params.prop == 'add') {
                    this.formData.dd.push({})
                }
                console.log(params)
            }
		}
	}

</script>
<style>
    .fd_form .fd_form .el-col-24 {
        margin-top: 8px;
    }
    .fd_imgs_item {
        padding-right: 55px;
    }
    .fd_list .fd_list_item {
       overflow-x: scroll;
       width: 100%;
    }
</style>
