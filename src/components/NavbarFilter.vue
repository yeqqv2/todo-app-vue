<template>
    <nav class="filter-nav">
        <button @click="filterGuncelle('hepsi')" :class="{ active: aktifSekme === 'hepsi' }">Bütün Görevler</button>
        <button @click="filterGuncelle('tamamlandi')" :class="{ active: aktifSekme === 'tamamlandi' }">Tamamlanan
            Görevler</button>
        <button @click="filterGuncelle('yapiliyor')" :class="{ active: aktifSekme === 'yapiliyor' }">Devam Eden
            Görevler</button>
    </nav>
</template>

<script>
export default {
    props: ['aktifSekme'],
    methods: {
        filterGuncelle(durum) {
            this.$emit('filterDurum', durum)
        }
    }

}
</script>

<style>
.filter-nav button {
    padding: 30px 10px;
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
}

.filter-nav button.active {
    color: black;
}
</style>