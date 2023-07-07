<template>
    <BigClock>
    </BigClock>
    <CountryList>
    </CountryList>
    <MotionsTab>
    </MotionsTab>
</template>

<script>
import BigClock from './BigClock.vue'
import CountryList from './CountryList.vue'
import MotionsTab from './MotionsTab.vue'

export default {
    name: 'Session',
    components: {
        BigClock,
        CountryList,
        MotionsTab
    }
}
</script>
