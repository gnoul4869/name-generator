<script setup lang="ts">
import { Gender, Popularity, Length, nameData, colors } from '@/data';

interface Options {
    gender: Gender;
    popularity: Popularity;
    length: Length;
}

const options = ref<Options>({
    gender: Gender.UNISEX,
    popularity: Popularity.TRENDY,
    length: Length.LONG,
});

const names = ref<string[]>([]);

interface OptionsData {
    id: number;
    type: string;
    buttons: Gender[] | Popularity[] | Length[];
}

const optionsData = computed<OptionsData[]>(() =>
    Object.keys(options.value).map((opt, idx) => {
        const buttons =
            opt === 'gender' ? Object.values(Gender) : opt === 'popularity' ? Object.values(Popularity) : Object.values(Length);

        return {
            id: idx,
            type: opt,
            buttons,
        };
    })
);

const generateNames = () => {
    const filteredNames = nameData.filter(
        (n) =>
            n.gender === options.value.gender &&
            n.popularity === options.value.popularity &&
            (options.value.length === Length.ALL ? true : n.length === options.value.length)
    );

    names.value = filteredNames.map((n) => n.name);
};

watch(
    names,
    () => {
        for (const name of names.value) {
            const nameCard: HTMLElement = document.querySelector(`#${name}`);
            if (nameCard) {
                const index: number = Math.floor(Math.random() * colors.length);
                nameCard.style.color = colors[index];
            }
        }
    },
    {
        flush: 'post',
    }
);
</script>

<template>
    <div class="container">
        <h1>Name Generator</h1>
        <div class="options-container">
            <div v-for="option in optionsData" :key="option.id">
                <Option :option="option" :options="options" />
            </div>
            <button class="main" @click="generateNames">Generate</button>
        </div>
        <div class="cards-container">
            <div v-for="name in names" :key="name" class="card" :id="name">
                <h4>{{ name }}</h4>
            </div>
        </div>
    </div>
</template>

<style lang="scss">
@import '@/assets/styles';

body {
    @include bg-green-gradient;
}

button {
    &.main {
        @include font(1rem, bold);
        color: $vue-green;
        background: white;
        border-radius: 6.5rem;
        border: none;
        outline: 0;
        box-shadow: rgba(0, 0, 0, 0.19) 0px 10px 20px, rgba(0, 0, 0, 0.23) 0px 6px 6px;
        padding: 0.75rem 4rem;
        margin-top: 1rem;
        cursor: pointer;
    }
}

.container {
    font-family: Arial, Helvetica, sans-serif;
    color: $slite-black;
    max-width: 50rem;
    margin: 0 auto;
    text-align: center;

    h1 {
        font-size: 3rem;
    }
}

.options-container {
    @include bg-green-gradient;
    border-radius: 2rem;
    padding: 1rem;
    widows: 95%;
    margin: 0 auto;
    margin-top: 4rem;
    position: relative;
    box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
}

.cards-container {
    display: flex;
    flex-wrap: wrap;
    margin-top: 3rem;
    justify-content: center;

    .card {
        @include bg-green-gradient;
        color: $slite-black;
        width: 28%;
        border-radius: 1rem;
        padding: 0.5rem;
        margin: 0.75rem;
        box-shadow: rgba(0, 0, 0, 0.15) 0px 5px 15px 0px;
    }
}
</style>
