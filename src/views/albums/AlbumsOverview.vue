<template>
    <div>
        <div>
            <h1>Albums</h1>
            <router-link to="/albums-create" tag="button">
                <v-icon>mdi-plus-circle </v-icon>
            </router-link>
        </div>
        <ul>
            <li v-bind:key="album.id" v-for="album in albums">
                {{album.title}}
            </li>
        </ul>
    </div>
</template>

<script>
    import restApi from '../../api/api'
    export default {
        components: { },
        mounted() {
            this.fetchAlbums()
        },
        data () {
            return {
                albums: []
            }
        },
        methods: {
            fetchAlbums() {
                restApi.get('albums')
                    .then((result) => {
                        this.albums = result.data
                    })
            }
        }
    };
</script>
