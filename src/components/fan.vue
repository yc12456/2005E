<template>
    <div class="aaaa">
    <div>
        <div>
            
        </div>
    </div>
</div>
</template>

<script>
export default {
    data() {
        return {
   
};
    },
    mounted() {
   
},
    methods: {
    
},
computed:{
    num(){
        return this.list.slice(this.pagesize*(this.currentPage4 - 1),
        this.pagesize*this.currentPage4)
    }
}
};
</script>

<style lang='scss'>
.aaaa{
    width: 100%;
}
</style>
