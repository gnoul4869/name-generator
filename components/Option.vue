<script setup lang="ts">
import { Gender, Popularity, Length } from '@/data';

defineProps<{
    option: {
        id: number;
        type: string;
        buttons: Gender[] | Popularity[] | Length[];
    };
    options: {
        gender: Gender;
        popularity: Popularity;
        length: Length;
    };
}>();

const upperCaseFirstLetter = (s: string) => {
    return s.charAt(0).toUpperCase() + s.slice(1);
};
</script>

<template>
    <div class="option">
        <h3>{{ upperCaseFirstLetter(option.type) }}</h3>
        <div class="buttons-container">
            <button
                v-for="btn in option.buttons"
                :key="btn"
                :class="options[option.type] === btn && 'active'"
                @click="options[option.type] = btn"
            >
                {{ upperCaseFirstLetter(btn) }}
            </button>
        </div>
    </div>
</template>

<style lang="scss">
@import '@/assets/styles';

.option {
    margin-bottom: 2rem;

    .buttons-container {
        button {
            @include font(1rem, bold);
            color: $slite-black;
            background-color: white;
            outline: 0.15rem solid $vue-green;
            border: none;
            padding: 0.75rem;
            width: 12rem;
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
}
</style>
