<template>
    <v-container>
        <v-row no-gutters>
            <v-col
                    md="6"
                    offset-md="3">
                <v-card  class="pa-2"
                         color="primary"
                         outlined
                         tile>
                    <v-card-title>
                        <v-row no-gutters>
                            <v-col
                                    md="1">
                                <router-link to="/albums-create" tag="button">
                                    <v-icon>mdi-plus-circle </v-icon>
                                </router-link>
                            </v-col>
                            <v-col justify="center" md="12">Albums</v-col>
                        </v-row>
                    </v-card-title>
                    <v-card-text>
                        <v-list>
                            <v-list-item-group color="primary"
                                               v-for="album in albums"
                                               :key="album.title">
                                <v-list-item>
                                    <v-list-item-avatar>
                                        <v-icon>mdi-image</v-icon>
                                    </v-list-item-avatar>

                                    <v-list-item-content>
                                        <v-list-item-title v-text="album.title"></v-list-item-title>
                                    </v-list-item-content>

                                    <v-list-item-action>
                                        <v-col>
                                            <v-btn icon>
                                                <v-icon color="grey lighten-1">mdi-circle-edit-outline</v-icon>
                                            </v-btn>
                                            <v-btn v-on:click="deleteAlbum(album)" icon>
                                                <v-icon color="grey lighten-1">mdi-minus-circle-outline</v-icon>
                                            </v-btn>
                                        </v-col>

                                    </v-list-item-action>
                                </v-list-item>
                                <v-divider inset></v-divider>
                            </v-list-item-group>
                        </v-list>
                    </v-card-text>
                    <v-card-actions>
                        <v-row no-gutters>
                            <v-col
                                    md="2"
                                    offset-md="10">

                            </v-col>
                        </v-row>

                    </v-card-actions>
                </v-card>
            </v-col>
        </v-row>
    </v-container>
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
            },
            deleteAlbum: function(album) {
                this.albums = this.albums.filter(alb => alb.id !== album.id);
                restApi.delete('albums/'+album.id)
                    .then((result) => {
                        console.log(result)
                        if(result.status !== 200) {
                            this.albums.push(album)
                        }
                    })
            }
        }
    };
</script>
