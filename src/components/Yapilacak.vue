<template>
    <div class="yapilacak">
        <div class="baslik">
            <h2 :class="{ strike: yapilacak.yapildi }" @click="detayGoster = !detayGoster">{{ yapilacak.baslik }} </h2>
            <div class="icon">
                <router-link :to="{ name: 'YapilacakGuncelle', params: { id: yapilacak.id } }">
                    <span class="material-icons">edit_note</span>
                </router-link>
                <span class="material-icons done" @click="toggle">done</span>
                <span class="material-icons close" @click="yapilacakSil">close</span>
            </div>

        </div>
        <hr>
        <div v-if="detayGoster" class="detay">
            <p>{{ yapilacak.icerik }}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: ['yapilacak'],
    data() {
        return {
            detayGoster: false,
            uri: 'http://localhost:3000/yapilacaklar/' + this.yapilacak.id,
        }
    },
    methods: {
        yapilacakSil() {
            fetch(this.uri, { method: 'DELETE' })
                .then(() => this.$emit('sil', this.yapilacak.id))
                .catch((err) => console.log(err))
        },
        toggle() {
            fetch(this.uri, {
                method: 'PATCH',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ yapildi: !this.yapilacak.yapildi })
            }).then(() => {
                this.$emit('yapildi', this.yapilacak.id)
            }).catch((err) => console.log(err))
        }
    }
}
</script>

<style>
.yapilacak {
    margin: 20px auto;
    padding: 10px 50px;
    border-radius: 50px
}

h2 {
    cursor: pointer;
}

.baslik {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.detay {
    display: flex;
    justify-self: start;
    margin-top: 0;
    color: #8d99ae;
}

.material-icons {
    font-size: 25px;
    margin-left: 10px;
    color: #bbb;
    cursor: pointer;
}

.material-icons:hover {
    color: #aaa;
}

.done {
    color: #5ed4c6;
}

.done:hover {
    color: #2a9d8f;
}

.close {
    color: #d80032;
}

.close:hover {
    color: #a30026;
}

@keyframes strike {
    0% {
        width: 0;
    }

    100% {
        width: 100%;
    }
}

.strike {
    position: relative;
    color: #8d99ae;
}

.strike::after {
    content: ' ';
    position: absolute;
    top: 50%;
    left: 0;
    width: 100%;
    height: 2px;
    background: #2b2d42;
    animation-name: strike;
    animation-duration: 2s;
    animation-timing-function: linear;
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
}
</style>