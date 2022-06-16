<script setup lang="ts">
import { Gender, Popularity, Length, nameData, nameColors } from '@/data';

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

const upperCaseFirstLetter = (s: string) => {
    return s.charAt(0).toUpperCase() + s.slice(1);
};

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
                const index: number = Math.floor(Math.random() * nameColors.length);
                nameCard.style.color = nameColors[index];
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
            <div class="option">
                <h3>Gender</h3>
                <div class="buttons-container">
                    <button
                        v-for="gen in Gender"
                        :key="gen"
                        :class="gen === options.gender && 'active'"
                        @click="options.gender = gen"
                    >
                        {{ upperCaseFirstLetter(gen) }}
                    </button>
                </div>
            </div>
            <div class="option">
                <h3>Popularity</h3>
                <div class="buttons-container">
                    <button
                        v-for="pop in Popularity"
                        :key="pop"
                        :class="pop === options.popularity && 'active'"
                        @click="options.popularity = pop"
                    >
                        {{ upperCaseFirstLetter(pop) }}
                    </button>
                </div>
            </div>
            <div class="option">
                <h3>Length</h3>
                <div class="buttons-container">
                    <button
                        v-for="len in Length"
                        :key="len"
                        :class="len === options.length && 'active'"
                        @click="options.length = len"
                    >
                        {{ upperCaseFirstLetter(len) }}
                    </button>
                </div>
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
$slite-black: #444;
$vue-green: #0faf87;

@mixin bg-green-gradient {
    background: rgb(51, 240, 250);
    background: linear-gradient(90deg, rgba(51, 240, 250, 0.6) 0%, rgba(0, 255, 19, 0.2) 100%);
}

body {
    @include bg-green-gradient;
}

button {
    &.main {
        color: $vue-green;
        background: white;
        border-radius: 6.5rem;
        border: none;
        outline: 0;
        box-shadow: rgba(0, 0, 0, 0.19) 0px 10px 20px, rgba(0, 0, 0, 0.23) 0px 6px 6px;
        padding: 0.75rem 4rem;
        font-size: 1rem;
        font-weight: bold;
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

    .option {
        margin-bottom: 2rem;
    }
}

.buttons-container {
    button {
        color: $slite-black;
        background-color: white;
        outline: 0.15rem solid $vue-green;
        border: none;
        padding: 0.75rem;
        width: 12rem;
        font-size: 1rem;
        font-weight: bold;
        cursor: pointer;

        &:first-child {
            border-radius: 1rem 0 0 1rem;
        }

        &:last-child {
            border-radius: 0 1rem 1rem 0;
        }

        &.active {
            background-color: $vue-green;
            color: white;
        }
    }
}

.cards-container {
    display: flex;
    flex-wrap: wrap;
    margin-top: 3rem;
    justify-content: center;

    .card {
        @include bg-green-gradient;
        width: 28%;
        color: mediumvioletred;
        border-radius: 1rem;
        padding: 0.5rem;
        margin: 0.75rem;
        box-shadow: rgba(0, 0, 0, 0.15) 0px 5px 15px 0px;
    }
}
</style>
