<template>
    <div class="contain" style="width: 100%; border-bottom: 1px solid lightgrey">
        <div class="containerNote">
            <button @click="delete_notes(note.id, index)"
            >
                <i class="fas fa-trash"></i>
            </button>
            <div
                    @click="clickNote(note)"
                    class="note"
            >
                <div style="display: flex; align-items: center; text-align: right" >
                    <i class="far fa-dot-circle"></i>
                    <article class="textNote">
                        {{ note.content.length > 10 ? note.content.substring(0, 10) +'...' : note.content }}
                    </article>
                </div>
                <div style="text-align: left; color: grey; font-size: 80%; font-style: italic; padding-top: 10px">{{moment(note.updated_at).format('LLL')}}</div>
            </div>
        </div>
    </div>

</template>

<style scoped>

    div{
        text-align: left !important;
    }
    .textNote{
        margin-left: 5px;
    }
    .note{
        cursor: pointer;
        align-items: center;
        padding: 10px;
        transition: ease-in-out 0.3s;
        width: 100%;
    }

    .containerNote{
        display: flex;
        width: 100%;
        position: relative;
        transform: translateX(-50px);
        transition: ease-in-out 0.3s;
    }

    /*.containerNote:hover{*/
    /*    transform: translateX(0px);*/

    /*}*/
    

    .contain{
        cursor: pointer;
    }


    .contain:hover .containerNote{
        transform: translateX(0px);

    }

    button{
        width: 70px;
        background: none;
        border: none;
        color: #ff4211;
        outline: none;
        font-size: 30px;
        cursor: pointer;
    }

</style>
<script>
    import { mapActions, mapMutations} from 'vuex'

    export default {
        props:{
            note:{
                type: Object
            },
            index: {

            }
        },

        methods: {
            ...mapActions({ delete_notes :'delete_notes'}),
            clickNote(note){
                this.$emit('noteClick', note)
            },

        }
    }
</script>