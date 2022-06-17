<template>
    <div class="notes">
        <div class="note" :class="{ 'note--full': !grid }" v-for="(item, idx) in data" :key="idx">
            <button class="close-btn" @click="removeItem(idx)">X</button>
            <div class="note-header">
                <p>{{ item.title }}</p>
            </div>
            <div class="item-body">
                <p>{{ item.description }}</p>
                <span>{{ item.date }}</span>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'NotesComp',
    props: {
        data: {
            type: Array,
            required: true
        },
        grid: {
            type: Boolean,
            required: true
        }
    },
    
    methods: {
        removeItem(index) {
            this.$emit('removeNote', index);
        }
    },
}
</script>
<style lang="scss">
    .notes {
        display: flex;
        align-items: center;
        justify-content: space-between;
        flex-wrap: wrap;
        padding: 40px 0;
    }
    
    .note {
        width: 48%;
        padding: 20px;
        margin-bottom: 20px;
        background-color: #fff;
        position: relative;
        transition: 0.25s;
        
        &--full {
            width: 100%;
            text-align: center;
        }
        
        &:hover {
            box-shadow: 0 30px 30px rgba(0,0,0,0.04);
            transform: translate(0, -6px);
        }
    }
    
    .note-header {
        p {
            font-size: 22px;
            color: #402caf;
        }    
    }
    
    .note-body {
        p {
            margin: 20px 0;
        }
        
        span {
            font-size: 14px;
            color: #999;
        }
    }
    
    .close-btn {
        cursor: pointer;
        position: absolute;
        top: 0;
        right: 0;
        display: flex;
        align-items: center;
        justify-content: center;
        background-color: transparent;
        border: none;
        color: darkred;
    }
</style>