<script>
export default {
    props: {
        themeClass: {
            type: String,
            required: true
        },
        isDarkMode: {
            type: Boolean,
            required: true
        },
        toggleTheme: {
            type: Function,
            required: true
        }
    }
};
</script>

<template>
    <nav class="navbar navbar-expand-lg fixed-top py-3">
        <div class="container-fluid">
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
                aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">

                <span style="cursor: pointer;" @click="toggleTheme" class="theme-toggle">
                    {{ isDarkMode ? 'Light Mood ☀️' : 'Dark Mood 🌙' }}
                </span>

            </div>
        </div>
    </nav>

</template>

<style></style>