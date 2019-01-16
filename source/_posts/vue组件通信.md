---
title: vue组件通信
tags: 学习
categories: 日记
---
一
1.父向子组件通信
通过props传值

父组件
```
<template>
	<header-box :header-title="title">子组件</header-box>
</template>
<script>
import header from "./header";
export default{
		name:'index',
		data(){
			return{
				title:'首页'
			}
		},
		components：{
			'header-box':header
		}
	}
</script>
```
子组件
```
<template>
	<header>{{textTitle}}</header>
</template>
<script>
export default{
	name:'header',
	props:["headerTitle"],
	data(){
		return{
			textTitle:this.headerTitle
		}
	}
}
</script>
```
2.子组件向父组件通信
通过$on,$emit

子组件
```
<template>
	<button @click="incrementCounter">{{num}}</button>
</templete>
<script>
export default{
	name:'button',
	data(){
		return{
			num:0,
		}
	},
	metheds:{
		incrementCounter：function(){
			this.$emit("change-value",this.num++)
		}
	}
}
</script>
```

父组件
```
<template>
	<button-center @change-value="num"></button-center>
</template>
<script>
import button from "./button"
export default{
	name:'parent',
	data(){
		return{
			counter:0,
		}
	},
	components:{
		"buttonCenter":button
	},
	metheds:{
		num:function(){
			this.counter++
		}
	}
}
<script>
```