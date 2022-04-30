<template>
<p v-if="pending">Loading...</p>
<table v-else>
    <tr>
        <th>rank</th>
        <th>name</th>
        <th>igt</th>
        <th>rta</th>
        <th>date</th>
        <th>link</th>
    </tr>
    <Run v-for="(run, index) in data.data.runs.filter(run => run.run.times.primary.match(/\d+(?=H)/) >= 3).reverse()" :run="run.run" :index="index + 1"/>
</table>
</template>

<script setup>
const { data, pending } = useLazyFetch("https://www.speedrun.com/api/v1/leaderboards/j1npme6p/category/mkeyl926?var-jlzkwqlz=mln68v0q&var-r8rg67rn=21d4zvp1");
</script>

<style>
</style>