## 音视屏标签学习
### 一、基本概念
> 视屏：连续的画面、特定的格式编码、媒体流
> 音频：特定格式编码、媒体流
### 二、格式
> 视频：mp4\ogv\webm
> 音频：mp3\ogg\wav
### 三、历史
> 早期使用flash、html后使用video\audio
### 四、使用案例
```
<!--
width :宽度
controls:使用控制器
loop:循环次数  -1位无数次
poster:视屏播放前显示的封面
preload:页面加载完成后主动加载视屏数据

-->

<!--写法一-->
<video src="../ime.mp4" width="640"  autoplay="autoplay" loop="1" preload  controls="controls" poster="../1.jpg">不支持视屏</video>
<!--写法二-->
<video width="640" autoplay="autoplay" loop="1"  controls="controls" >
    <!--
    第一个失效的时候播放第二个
    type：解码器
    -->
    <source src="../ime.mp4" type="video/mp4"/>
    <source src="http://video.mukewang.com/mk.mp4" type="video/mp4"/>
    不支持视屏
</video>

<!--和视屏大致一直-->
<audio src="" >
    不支持音频
</audio>

```

#### 五、事件、属性、方法
```
<body>
<!--
preload:auto|meta|none
auto:加载源数据和视屏的数据; meta:加载源数据 ; none:不加载数据
-->
 <button  id="start">开始</button>
 <button  id="pause">暂停</button>
<video  id="video" src="../ime.mp4"  preload="" controls="controls">不支持视屏</video>
<script>
     let video=document.getElementById('video');
   /*以下都是事件*/
        [
         "loadstart",
         "progress",
         "suspend",
         "abort",
         "emptied",
         "stalled",
         "loadedmetadata",/*加载一份源数据  和preload有关*/
         "loadeddata",
         "canplaythrough",
         "playing",
         "waiting",
         "seeking",
         "enbed",
         "durationchange",
         "timeupdate",
         "play",
         "seeked",
         "ratechange",
         "volumechange",
         "pause",
         "error",
         "canplay"
      ].forEach(v=>{
          video['on'+v]=()=> {
              console.log(v)
          }
      });

    /*属性和方法*/
    let start=document.getElementById('start');
    let pause=document.getElementById('pause');
     start.onclick=()=>{
         video.play(); //开始
     }
     pause.onclick=()=>{
         video.pause();//暂停
     }
     video.onloadedmetadata=()=>{
         console.log("视屏地址"+video.currentSrc);
         console.log("视屏总时长"+video.duration);
         console.log("视屏播放速率"+video.playbackRate);
         console.log("是否暂停"+video.paused);
         console.log("是否结束"+video.ended);
         console.log("是否静音"+video.muted);
     }

     video.ontimeupdate=()=>{
         console.log("视屏当前时间"+video.currentTime);
         console.log("当前缓冲量"+video.buffered.end(0));
     }

     video.onvolumechange=()=>{
         console.log("当前音量"+video.volume);
     }

     //通过属性和方法完全可以实现自定义样式
```

#### 六、插件
> http://www.jplayer.cn/