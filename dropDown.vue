<template>
<div class="content">
    <div class="select">
        <p>所有选项</p>
        <ul>
            <li data-value="所有选项" class="selected">所有选项</li>
            <li data-value="html">html</li>
            <li data-value="css">css</li>
            <li data-value="jQuery">jQuery</li>
            <li data-value="javascript">javascript</li>
        </ul>
    </div>
</div>
</template>
 
<script>
    export default {
        data() {
            return {
                show:true,
            }
        },
        mounted(){
     $(document).ready(function(){
    //点击P标签切换下拉框
    $('.select > p').on('click', function(event) {
        $('.select').toggleClass('open');
        event.stopPropagation();
    });
    //点击li标签,赋值、切换下拉框、给选中的li标签添加选中样式同级元素移除选中样式、阻止事件冒泡
    $('.select ul li').on('click',function(event){
        var _this = $(this);
        $('.select p').text(_this.attr('data-value'));
        $('.select').toggleClass('open');
        _this.addClass('selected').siblings().removeClass('selected');
        event.stopPropagation();
    })
    //点击除下拉框的其它地方，收起下拉框
    $(document).on('click',function(){
        $('.select').removeClass('open');
    })
});       

        },
        
    }
</script>
 
 <style>
body,p,ul {
    margin: 0;
    padding: 0;
}           
body {
    background-color: #0c9;
    color: #333;
}           
.content {
    padding-top: 5%;
}           
.content .select {
    width: 300px;
    height: 40px;
    margin: 0 auto;
    font-family: "Microsoft Yahei";
    font-size: 16px;
    background-color: #fff;
    position: relative;
}
/*transform(缩放、旋转、平移)，显示的是最终效果，没有动画过程*/
/*transition是对元素本身的属性(比如：width、height)设置动画效果*/          
.content .select:after {
    content: '';
    display: block;
    width: 10px;
    height: 10px;
    border-left: 1px #ccc solid;
    border-bottom: 1px #ccc solid;
    position: absolute;
    top: 11px;
    right: 12px;
    transform: rotate(-45deg);
    transition: transform .3 ease-out,top .3s ease-out;
}           
.content .select p {
    padding: 0 15px;
    line-height: 40px;
    cursor: pointer;
}
/*设置下拉框收起时的高度过渡动画*/         
.content .select ul {
    list-style-type: none;
    background-color: #fff;
    width: 100%;
    overflow-y: auto;
    position: absolute;
    top: 40px;
    left: 0;
    max-height: 0;
    transition: max-height .3s ease-out;
}           
.content .select ul li {
    padding: 0 15px;
    line-height: 40px;
    cursor: pointer;
}           
.content .select ul li:hover {
    background-color: #e0e0e0;
}           
.content .select ul li.selected {
    background-color: #39f;
    color: #fff;
}
/*下拉框展开时调用动画slide-down*/
/*transform-origin设置缩放下拉框的基点位置*/            
.content .select.open ul {
    max-height: 250px;
    -webkit-animation: slide-down .5s ease-in;
    transition: max-height .3s ease-in;
    transform-origin: 50% 0; 
}
/*设置展开时下拉箭头的旋转动画*/          
.content .select.open:after {
    transform: rotate(-225deg);
    top: 18px;
    transition: all .3s ease-in-out;
}
/*为下拉框展开时添加名称为slide-down的关键帧动画*/
@-webkit-keyframes slide-down{
    0%{transform: scale(1,0);}
    25%{transform: scale(1,1.2);}
    50%{transform: scale(1,0.85);}
    75%{transform: scale(1,1.05);}
    100%{transform: scale(1,1);}
}
</style>
