<template>
<tr>
    <td>{{ props.index }}</td>
    <td v-if="pending">Loading name...</td>
    <td v-else>{{ data.data.names.international }}</td>
    <td>{{ formatTime(props.run.times.primary) }}</td>
    <td>{{ formatTime(props.run.times.realtime) }}</td>
    <td>{{ props.run.date.replace("-", "/").replace("-", "/") }}</td>
    <td><a :href="props.run.weblink"><img src="/assets/favicon.ico"></a></td>
</tr>
</template>

<script setup>
const props = defineProps(["run", "index"]);
const id = props.run.players[0].id;
const { data, pending } = useLazyFetch(`https://www.speedrun.com/api/v1/users/${id}`);

function formatTime(time) {
    let h = time.match(/\d+(?=H)/);
    let m = time.match(/\d+(?=M)/) ?? "00";
    let s = time.match(/(?<=M)\d+/) ?? "00";
    let ms = time.match(/(?<=\.)\d+(?=S)/) ?? "000";
    m = ("0" + m).slice(-2);
    s = ("0" + s).slice(-2);
    return(`${h}:${m}:${s}.${ms}`);
}
</script>