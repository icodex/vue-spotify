<template>
  <div
    v-scroll
    @vScroll="loadMore($event, playlists.next, getPlaylists)"
  >
    <media-container>
      <media-object
        v-for="(item) in playlists.items"
        :key="item.id"
        :id="item.id"
        :uri="item.uri"
        :coverImg="item.images"
        :name="item.name"
        :type="item.type"
      />
    </media-container>
  </div>
</template>

<script>
  import {
    mapState,
    mapActions,
  } from 'vuex'

  import {loadMore} from '@/mixins'
  import MediaObject from '@/components/MediaObject'
  import MediaContainer from '@/components/MediaContainer'

  export default {
    name: 'search-playlist-view',

    mixins: [loadMore],

    components: {
      MediaObject,
      MediaContainer
    },

    computed: {
      ...mapState('search', [
        'playlists',
      ]),
    },

    methods: {
      ...mapActions({
        getPlaylists: 'search/getPlaylists',
      }),
    },
  }
</script>
