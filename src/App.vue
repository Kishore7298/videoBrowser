<template>
    <div class="container">
        <SearchBar @termChange="onTermChange"></SearchBar>
        <div class="row">
            <VideoDetail  :video="selectedVideo"  />
            <VideoList :videos='videos' @videoSelect='onVideoSelect'></VideoList>
        </div>
    </div>
</template>
<script>
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';
import axios from 'axios';
const API_KEY = 'AIzaSyANdPNy4cxBaRN0QKwuNaNv-eoJq9kQGH0';
export default {
    name:'App',
    components: {
        SearchBar,
        VideoList,
        VideoDetail
    },
    data:function () {
            return {videos:[], selectedVideo : null };
        }
    ,
    methods : {
        onTermChange : function(searchTerm){
            axios.get('https://www.googleapis.com/youtube/v3/search',{
                params: {
                    key: API_KEY,
                    type: 'video',
                    part: 'snippet',
                    q:searchTerm
                }
            }).then(response => this.videos = response.data.items);
        },
        onVideoSelect(video){
            this.selectedVideo = video;
        }

    }
};
</script>
