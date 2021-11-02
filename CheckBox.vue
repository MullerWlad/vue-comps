<template>
    <div class="container">
        <p>{{name}}</p>
        <p 
            v-bind:class="classes[index]" 
            v-for="(item, index) in list" 
            v-bind:key="(item, index)"
            @click="useIt(item, index)"
        >&bull; {{item}}</p>
    </div>
</template>
<script>
    export default {
        props: ["name", "list"],
        data() {
            return {
                checked: [],
                classes: []
            }
        },
        methods: {
            useIt(value, index) {
                if (this.checked.includes(value)) {
                    this.checked = this.checked.filter(item => {
                        return item != value
                    })
                    this.$set(this.classes, index, "unchecked")
                } else {
                    this.checked.push(value)
                    this.$set(this.classes, index, "checked")
                }
                this.$emit('value', this.checked)
            }
        },
        created() {
            this.list.forEach(item => {
                this.classes.push("unchecked")
            })
        }
    }
</script>
<style scoped>
    .container > p {
        font-family: "gilroy-medium";
    }
    .container > p:first-child {
        font-size: 18px;
        color: #323232;
    }
    .container > p.unchecked {
        font-size: 18px;
        color: #323232;
        cursor: pointer;
    }
    .container > p.checked {
        font-size: 18px;
        color: #94BE00;
        cursor: pointer;
    }
</style>