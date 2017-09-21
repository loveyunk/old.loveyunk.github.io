---
layout: post
title: 封装element-ui的dialog组件
---

封装组件：
{% highlight ruby %}
<template>
    <div class="dialog-container">
        <el-dialog
            title="title"
            :visible.sync="visible"
            @close="$emit('update:show', false)"
            :show="show">
            <span>this is a dialog.</span>
        </el-dialog>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                visible: this.show
            };
        },
        props: {
            show: {
                type: Boolean,
                default: false
            }
        },
        watch: {
            show () {
                this.visible = this.show;
            }
        }
    };
</script>
{% endhighlight %}
使用：
{% highlight ruby %}
<template>
    <div class="container">
        <z-dialog :show.sync="show"></z-dialog>
        <button @click="open">click</button>
    </div>
</template>

<script>
    import ZDialog from './dialog';

    export default {
        data () {
            return {
                show: false
            };
        },
        methods: {
            open () {
                this.show = true;
            }
        },
        components: {
            ZDialog
        }
    };
</script>
{% endhighlight %}