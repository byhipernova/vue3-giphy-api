<template>
    <div class="img-wrapper">
        <div class="img-inner">
            <img :src="'https://i.giphy.com/media/'+data.id+'/giphy.webp'" :alt="data.title">
            {{ data.id }}
            <div class="description">
                {{ data.title }}
                <button :data-url="'https://i.giphy.com/media/'+data.id+'/giphy.webp'" @click="downloadHandle" download><img class="download-icon"
                        src="https://www.svgrepo.com/show/138917/download.svg" alt="Download"></button>
            </div>
        </div>
    </div>
</template>

<script>
import FileSaver from 'file-saver';
export default {
    props: {
        data: Object
    },
    methods:{
        downloadHandle(e){
            FileSaver.saveAs(e.currentTarget.getAttribute('data-url'), "giphy.webp");
        }
    }
}
</script>

<style lang="scss">
.img-wrapper {
    width: 25%;
    height: 300px;
    padding: 1rem;

    .img-inner {
        position: relative;
        overflow: hidden;
        height: 100%;

        &:hover {
            .description {
                bottom: 0;
            }
        }

        img {
            height: 300px;
            object-fit: cover;
        }

        .description {
            position: absolute;
            bottom: -100px;
            background: rgba($color: #000000, $alpha: .6);
            color: white;
            width: 100%;
            padding: .5rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: .5rem;
            transition: .3s;

            button {
                display: flex;
                background: transparent;
                padding: 0;
                border-width: 0;
                outline-width: 0;
                cursor: pointer;

                .download-icon {
                    width: 1.5rem;
                    height: auto;
                    filter: invert(100%) sepia(0%) saturate(7488%) hue-rotate(14deg) brightness(95%) contrast(96%);
                }
            }
        }
    }

    @media screen and (max-width: 576px) {
        width: 100%;
    }

    @media screen and (min-width: 576px) and (max-width: 992px) {
        width: 50%;
    }

    @media screen and (min-width: 992px) and (max-width: 1200px) {
        width: 33.3333%;
    }

    img {
        width: 100%;
    }
}
</style>