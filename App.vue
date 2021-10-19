<template>
    <section>
        <div class="cronometro">
            <div class="visor" v-if="seconds == 0">00:00:00</div>
            <div class="visor" v-if="seconds != 0">{{ hours }}:{{ mins }}:{{ secs }}</div>
            <div class="controles">
                <button @click="start">Iniciar</button>
                <button @click="stop">Parar</button>
                <button @click="restart">Reiniciar</button>
            </div>
        </div>
    </section>
</template>

<script>
export default {
    name: "app",
    components: {},
    data() {
        return {
            seconds: 0,
            interval: null,

            hours: 0,
            mins: 0,
            secs: 0,
        };
    },
    methods: {
        timer() {
            this.seconds++;

            this.hours = Math.floor(this.seconds / 3600);
            this.mins = Math.floor((this.seconds - this.hours * 3600) / 60);
            this.secs = this.seconds % 60;

            if (this.hours < 10) this.hours = "0" + this.hours;
            if (this.mins < 10) this.mins = "0" + this.mins;
            if (this.secs < 10) this.secs = "0" + this.secs;
        },
        start() {
            if (this.interval) {
                return;
            }
            this.interval = setInterval(this.timer, 1000);
        },
        stop() {
            clearInterval(this.interval);
            this.interval = null;
        },
        restart() {
            this.stop();
            this.seconds = 0;
            this.hours = 0;
            this.mins = 0;
            this.secs = 0;
        },
    },
};
</script>

<style>
:root {
    --primary: #dc143d;
    --dark: #1f2937;
    --darkdark: #111827;
    --light: #f3f4f6;
}

* {
    margin: 0;
    box-sizing: border-box;
    font-family: "Fira sans", sans-serif;
}

body {
    background-color: var(--dark);
    color: var(--light);
}

.cronometro {
    text-align: center;
    background-color: var(--darkdark);
    width: 100%;
    max-width: 360px;
    margin: 4rem auto;
    padding: 1rem 2rem;
    border-radius: 1rem;
}

.cronometro .visor {
    font-size: 5rem;
    font-weight: 300;
    margin-bottom: 1rem;
}

.controles {
    display: flex;
    align-items: center;
    justify-content: center;
}

.controles button {
    appearance: none;
    background: none;
    outline: none;
    border: none;
    cursor: pointer;

    margin: 0 0.5rem;
    padding: 0.5rem 1rem;
    border-radius: 0.5rem;

    color: #fff;
    background-color: var(--primary);

    transition: 0.4s;
    user-select: none;
}

.controles button:hover {
    opacity: 0.7;
}

.controles button:active {
    background-color: var(--dark);
}
</style>
