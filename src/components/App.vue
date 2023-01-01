<template>
    <div class="d-flex flex-fill justify-content-center">
        <div class="card w-100 p-4">
            <div class="card-body rounded border border-dark shadow-lg">
                <h1 class="fw-bold">Online Party Games</h1>
                <p>All of the following games can be played online without any preparation.</p>
                <hr />
                <div class="d-flex justify-content-end">
                    <button class="btn btn-dark dropdown-toggle" type="button" data-bs-toggle="dropdown"
                        aria-expanded="false">Sort by:</button>
                    <ul class="dropdown-menu">
                        <li class="dropdown-item clickable" @click="game_list.sort(sortByNameAsc)">Name:
                            A-Z
                        </li>
                        <li class="dropdown-item clickable" @click="game_list.sort(sortByNameDesc)">
                            Name:
                            Z-A</li>
                        <li class="dropdown-item clickable" @click="game_list.sort(sortByMinPlayersAsc)">
                            Minimum Players: Low to high</li>
                        <li class="dropdown-item clickable" @click="game_list.sort(sortByMinPlayersDesc)">
                            Minimum Players: High to low</li>
                    </ul>
                </div>
                <div class="table-responsive rounded">
                    <table class="table table-hover">
                        <thead>
                            <tr>
                                <th scope="col">

                                </th>
                                <th scope="col">
                                    Name
                                </th>
                                <th scope="col">
                                    Min Players
                                </th>
                                <th scope="col">
                                    Max Players
                                </th>
                            </tr>
                        </thead>
                        <tbody>
                            <Game :data="game" v-for="game in game_list" />
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { Dropdown } from "bootstrap"
import Game from './Game.vue';
import games from '/assets/games.json';

const game_list = ref(games.list);

function sortByNameAsc(a, b) {
    if (a.title.toLowerCase() > b.title.toLowerCase()) {
        return 1;
    }
    if (a.title.toLowerCase() < b.title.toLowerCase()) {
        return -1;
    }
    return 0;
}

function sortByNameDesc(a, b) {
    if (a.title.toLowerCase() > b.title.toLowerCase()) {
        return -1;
    }
    if (a.title.toLowerCase() < b.title.toLowerCase()) {
        return 1;
    }
    return 0;
}

function sortByMinPlayersAsc(a, b) {
    if (a.players_min > b.players_min) {
        return 1;
    }
    if (a.players_min < b.players_min) {
        return -1;
    }
    return 0;
}

function sortByMinPlayersDesc(a, b) {
    if (a.players_min > b.players_min) {
        return -1;
    }
    if (a.players_min < b.players_min) {
        return 1;
    }
    return 0;
}

onMounted(() => {
    game_list.value.sort(sortByNameAsc)
})
</script>