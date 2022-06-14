<script setup lang="ts">
enum Gender {
    MALE = 'male',
    UNISEX = 'unisex',
    FEMALE = 'female',
}

enum Popularity {
    TRENDY = 'trendy',
    UNIQUE = 'unique',
}

enum Length {
    LONG = 'long',
    FULL = 'full',
    SHORT = 'short',
}

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
</script>

<template>
    <div class="container">
        <h1>Name Generator</h1>
        <div class="options-container">
            <div class="option">
                <h3>Gender</h3>
                <div class="buttons-container">
                    <button :class="options.gender === Gender.MALE && 'active'">Male</button>
                    <button :class="options.gender === Gender.UNISEX && 'active'">Unisex</button>
                    <button :class="options.gender === Gender.FEMALE && 'active'">Female</button>
                </div>
            </div>
            <div class="option">
                <h3>Popularity</h3>
                <div class="buttons-container">
                    <button :class="options.popularity === Popularity.TRENDY && 'active'">Trendy</button>
                    <button :class="options.popularity === Popularity.UNIQUE && 'active'">Unique</button>
                </div>
            </div>
            <div class="option">
                <h3>Length</h3>
                <div class="buttons-container">
                    <button :class="options.length === Length.LONG && 'active'">Long</button>
                    <button :class="options.length === Length.FULL && 'active'">Full</button>
                    <button :class="options.length === Length.SHORT && 'active'">Short</button>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss">
body {
    background: rgb(51, 240, 250);
    background: linear-gradient(90deg, rgba(51, 240, 250, 0.6) 0%, rgba(0, 255, 19, 0.2) 100%);
}

.container {
    font-family: Arial, Helvetica, sans-serif;
    color: #444;
    max-width: 50rem;
    margin: 0 auto;
    text-align: center;

    h1 {
        font-size: 3rem;
    }
}

.options-container {
    background: rgb(51, 240, 250);
    background: linear-gradient(90deg, rgba(51, 240, 250, 0.7) 0%, rgba(0, 255, 19, 0.2) 100%);
    border-radius: 2rem;
    padding: 1rem;
    widows: 95%;
    margin: 0 auto;
    margin-top: 4rem;
    position: relative;

    .option {
        margin-bottom: 2rem;
    }
}

.buttons-container {
    button {
        color: #444;
        background-color: white;
        outline: 0.15rem solid #0faf87;
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
            background-color: #0faf87;
            color: white;
        }
    }
}
</style>
