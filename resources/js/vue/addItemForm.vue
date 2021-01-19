<template>
    <div class="addItem">
        <input type="text" v-model="item.name" />
        <font-awesome-icon 
            icon="plus-square"
            :class="[ item.name ? 'active' : 'inactive', 'plus' ]"
            @click="addItem()"
        />
    </div>
</template>
<script>
    export default {
        data: () => {
            return {
                item: {
                    name: ""
                }
            }
        },
        methods: {
            addItem() {
                if( this.item.name == '' ) {
                    return;
                }
                else {
                    axios.post('api/item/store', {
                        item: this.item
                    }).then(response => {
                        if(response.status == 201) {
                            this.item.name = ""
                            this.$emit('reloadList')
                        }
                    }).catch(error => {
                        console.log(error)
                    })
                }
            }
        }
    }
</script>

<style scoped>
    .addItem {
        display: flex;
        justify-content: center;
        align-items: center;
    }
    input {
        background: #f7f7f7;
        border: 0px;
        outline: none;
        padding: 5px;
        margin: 0 10px 0 0;
        widows: 100%;
    }
    .plus {
        font-size: 20px;
    }
    .active {
        color: #00ce25;
    }
    .inactive {
        color: #999;
    }
</style>