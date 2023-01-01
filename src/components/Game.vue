<template>
    <tr ref="thisTooltip" class="clickable position-relative" @click="openGame">
        <td>
            <img :src="props.data.image" width="56" height="56">
        </td>
        <td class="align-middle">
            <div class="d-flex flex-column">
                <span class="fw-bold">{{ props.data.title }}</span>
                <span class="text-muted">{{ props.data.description }}</span>
            </div>
        </td>
        <td class="align-middle"><span class="text-muted">{{ props.data.players_min }}</span></td>
        <td class="align-middle"><span class="text-muted">{{ max_players }}</span></td>
    </tr>
</template>

<script setup>
import { ref, computed } from 'vue';

const thisTooltip = ref(null);

const max_players = computed(() => {
    if (props.data.players_max == "-1") {
        return "∞"
    }
    return props.data.players_max
})

async function openGame() {
    window.open(props.data.url, '_blank');
}

const props = defineProps({
    data: {
        type: Object,
        required: true
    }
});
</script>