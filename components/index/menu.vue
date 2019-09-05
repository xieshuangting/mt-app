<template>
    <div class="m-menu">
        <dl class="nav" @mouseleave="mouseleave">
            <dt>全部分类</dt>
            <dd v-for="(item,idx) in menu" :key='idx' @mouseenter='enter($event)'>
                <i :class="item.type"></i>{{item.name}}<span class="arrow"></span>
            </dd>
        </dl>
        <div class="detail" v-if="kind" @mouseleave="sout" @mouseenter="sover">
            <template v-for="(item,idx) in curdetail.child">
                <h4 :key='idx'>{{item.title}}</h4>
                <span v-for="v in item.child" :key='v'>{{v}}</span>
            </template>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return {
            kind:'',
            menu:[{
                type:'food',
                name:'美食',
                child:[{
                    title:'美食',
                    child:['代金券','甜品饮品']
                }]
            },{
                type:'takeout',
                name:'外卖',
                child:[{
                    title:'美食',
                    child:['代金券','甜品饮品']
                }]
            },{
                type:'hotel',
                name:'酒店',
                child:[{
                    title:'美食',
                    child:['代金券','甜品饮品']
                }]
            }]
        }
    },
    computed:{
        curdetail:function(){
            return this.menu.filter(item=>item.type == this.kind)[0]
        }
    },
    methods:{
        mouseleave:function(){
            let left = this;
            self._timer = setTimeout(function(){
                self.kind = '';
            },150);
        },
        enter:function(e){
            this.kind = e.target.querySelector('i').className;
        },
        sover:function(){
            clearTimeout(this._timer);
        },
        sout:function(){
            this.kind = '';
        }
    }
}
</script>