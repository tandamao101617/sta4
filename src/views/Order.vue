<template>
    <div class="Order">
        <orderHeader/>
        <orderTable/>
    </div>
</template>

<script>
import orderHeader from './../components/orderHeader'
import orderTable from './../components/orderTable'

export default {
    name: 'Order',
    components: {
    orderHeader,
    orderTable,
  }
}
</script>

<style lang="less">
    
</style>

