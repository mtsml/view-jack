<template>
    <nav class="navbar navbar-dark bg-dark fixed-top px-0 py-1 z-depth-0">
        <div class="text-nowrap ml-1">
            <button 
                class="navbar-toggler"
                data-toggle="collapse"
                data-target="#sidebarMenu"
            >
                <i class="fas fa-bars fa-1x"></i>
            </button>
            <a class="navbar-brand" href="/">
                <strong>
                    {{ head }}
                </strong>
            </a>
        </div>
        <div id="sidebarMenu" class="collapse navbar-collapse">
            <ul class="navbar-nav ml-3 mr-auto" v-for="channel of channel_list" v-bind:key="channel.channel_id">
                <li class="nav-item">
                    <router-link class="nav-link" :to="{name: 'channel', params: {channel_id: channel.channel_id}}">
                        {{channel.channel_nm}}
                    </router-link>
                </li>
            </ul>
        </div>
    </nav>
</template>
<script>
import client from '../api/api'

export default {
    name: 'Header',
    props: {
        head: String
    },
    data: () => ({
        channel_list: []
    }),
    mounted() {
        client.getChannels()
            .then(response => this.channel_list = response.data.channel_list)
            .catch(error => alert(error))
    }
}
</script>