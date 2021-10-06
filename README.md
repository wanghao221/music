# ❤️使用 HTML、CSS 和 JS 创建在线音乐播放器❤️

![在这里插入图片描述](https://img-blog.csdnimg.cn/f56835370056479e8cd80298ff892904.png#pic_center)
<a href="https://github.com/wanghao221/music/blob/main/README.md#-%E5%AE%8C%E6%95%B4%E6%BA%90%E7%A0%81%E4%B8%8B%E8%BD%BD"><font size="5" color="#03a9f4"><b><u>直接跳到末尾</u></b></font></a>  **获取完整源码**

> <font color="#B8860B">**今天我将带着大家使用 HTML、CSS 和 JS创建 [音乐播放器](http://haiyong.site/yinyue)，没有使用任何其他库。我们的音乐播放器具有三个部分。主屏幕、播放器部分和播放列表部分。我们的主页部分有一个平滑的工作滑块，也有水平滚动。这个音乐播放器最好的部分是它最小化了音乐播放器。是的，您可以最小化和最大化播放器本身。使这个项目成为一个很棒的音乐播放器。**</font>

## 🎪 在线演示地址

[http://haiyong.site/yinyue](http://haiyong.site/yinyue)

## 🥇 完整代码结构
在我们开始编写代码之前。虽然它不是 Nodejs 应用程序，但我们至少应该看到它的文件夹结构。

![在这里插入图片描述](https://img-blog.csdnimg.cn/d8ac58504c0d46e9a354752bb96a0b84.png)
你可以看到我们有一个data.js文件，该文件包含我们的音乐相关数据。你可以在下面看到。

```js
let songs = [
    {
        name: 'song 1',
        path: 'assets/musics/Song 1.mp3',
        artist: 'artist 1',
        cover: 'assets/images/cover 1.png'
    },
    {
        name: 'song 2',
        path: 'assets/musics/Song 2.mp3',
        artist: 'artist 2',
        cover: 'assets/images/cover 2.png'
    },
    // 剩下8首歌曲格式同上
]
```
我们在这里存储了音乐相关数据。

然后现在让我们对主页部分进行编码。

## 🎯 home-section 首页部分
打开index.html和内部从编写基本的 HTML 结构开始。还链接style.css和两个 JS 文件。记得data.js在app.js. 否则我们将无法访问数据。

完成链接所有文件后，让我们创建第一件事。图像轮播。内部身体标签代码这个。

```html
<section class="home-section">
    <div class="carousel">
        <img src="assets/images/cover 1.png" class="active" alt="">
        <img src="assets/images/cover 2.png" alt="">
        <img src="assets/images/cover 3.png" alt="">
        <img src="assets/images/cover 4.png" alt="">
        <img src="assets/images/cover 5.png" alt="">
    </div>
</section>
```
注意 - 将旋转木马包裹在`home-section`元素内。

```css
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700;900&display=swap');

*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

:root{
    --background: #141414;
    --text-color: #fff;
    --primary-color: #63ff69;
    --secondary-color: #000;
    --alpha-color: rgba(0, 0, 0, 0.5);
    --shadow: 0 15px 40px var(--alpha-color);
}

html{
    background: var(--background);
    display: flex;
    justify-content: center;
}

body{
    width: 100%;
    height: 100vh;
    max-width: 375px;
    position: relative;
    background: var(--background);
    font-family: 'roboto', sans-serif;
    color: var(--text-color);
}

::-webkit-scrollbar{
    display: none;
}

.home-section{
    width: 100%;
    padding: 20px;
    height: 100%;
    padding-bottom: 100px;
    overflow-y: auto;
}

/* carousel */

.carousel{
    width: 100%;
    height: 200px;
    overflow: hidden;
    border-radius: 20px;
    box-shadow: var(--shadow);
    position: relative;
}

.carousel img{
    position: absolute;
    width: 100%;
    height: 100%;
    object-fit: cover;
    opacity: 0;
    transition: 1s;
}

.carousel img.active{
    opacity: 1;
}
```
您可以看到我们在这里使用了 CSS 变量，因此我们将来可以轻松更改此音乐播放器主题。

**输出**
![在这里插入图片描述](https://img-blog.csdnimg.cn/5e02e4835274417f9ff0ea5ca76c731a.png)

请注意，这是为移动视图设计的，这就是为什么我使用 chrome 检查器以移动尺寸查看它的原因。

现在创建水平滚动播放列表。放在`home-section`里面

**HTML**

```html
<h1 class="heading">最近播放</h1>
<div class="playlists-group">
	<div class="playlist-card">
		<img src="assets/images/cover 9.png" class="playlist-card-img" alt="">
		<p class="playlist-card-name">华语热歌</p>
	</div>
	<div class="playlist-card">
		<img src="assets/images/cover 2.png" class="playlist-card-img" alt="">
		<p class="playlist-card-name">古风戏腔</p>
	</div>
	//+3 
</div>
<h1 class="heading">根据你的喜好</h1>
<div class="playlists-group">
	<div class="playlist-card">
		<img src="assets/images/cover 12.png" class="playlist-card-img" alt="">
		<p class="playlist-card-name">失恋回忆</p>
	</div>
	<div class="playlist-card">
		<img src="assets/images/cover 12.png" class="playlist-card-img" alt="">
		<p class="playlist-card-name">经典老歌</p>
	</div>
	//+3 
</div>
```
**CSS**

```css
.heading{
    margin: 30px 0 10px;
    text-transform: capitalize;
    font-weight: 400;
    font-size: 30px;
}

/* playlists card */

.playlists-group{
    position: relative;
    width: 100%;
    min-height: 200px;
    height: auto;
    display: flex;
    flex-wrap: nowrap;
    overflow-x: auto;
}

.playlist-card{
    flex: 0 0 auto;
    max-width: 150px;
    height: 100%;
    margin-right: 20px;
}

.playlist-card-img{
    width: 100%;
    height: 150px;
    object-fit: cover;
    border-radius: 20px;
}

.playlist-card-name{
    width: 100%;
    text-align: justify;
    font-size: 20px;
    text-transform: capitalize;
    padding: 5px;
}
```
**输出**
![在这里插入图片描述](https://img-blog.csdnimg.cn/975b293d1475474a896ea93802835e18.png =200x)


我们完成了`home section`。但是我们的旋转木马还不起作用，所以让我们使用 js 让它工作。打开app.js文件并开始编码。

```javascript
const carousel = [...document.querySelectorAll('.carousel img')];

let carouselImageIndex = 0;

const changeCarousel = () => {
    carousel[carouselImageIndex].classList.toggle('active');

    if(carouselImageIndex >= carousel.length - 1){
        carouselImageIndex = 0;
    } else{
        carouselImageIndex++;
    }

    carousel[carouselImageIndex].classList.toggle('active');
}

setInterval(() => {
    changeCarousel();
}, 3000);
```
您可以看到我们的轮播元素，每 3 秒切换一次图像active类。

![在这里插入图片描述](https://img-blog.csdnimg.cn/5eea9a8c0f024c0eb9173622593677ef.gif =200x)


现在让我们制作我们的播放器部分。

## 🍖 player-section 播放器部分
首先使其最小化视图。

```html
<section class="music-player-section">

    <img src="assets/images/back.png" class="back-btn icon hide" alt="">
    <img src="assets/images/nav.png" class="nav-btn icon hide" alt="">

    <h1 class="current-song-name">song 1</h1>
    <p class="artist-name hide">artist 1</p>

    <img src="assets/images/cover 1.png" class="cover hide" alt="">

    <div class="seek-bar-container">
        <input type="range" class="music-seek-bar" value="0">
        <p class="current-time hide">00 : 00</p>
        <p class="duration hide">00 : 00</p>
    </div>

    <div class="controls">
        <span class="fas fa-redo"></span>
        <div class="main">
            <i class="fas fa-backward active"></i>
            <i class="fas fa-play active"></i>
            <i class="fas fa-pause"></i>
            <i class="fas fa-forward active"></i>
        </div>
        <input type="range" class="volume-slider" max="1" value="1" step="0.1">
        <span class="fas fa-volume-up"></span>
    </div>
</section>
```

如果你看到我们的播放器结构，你会注意到我们有很多hide元素的类。此类hide指示元素将在最小化视图中隐藏。我们为所有元素提供了相同的类，因此我们可以轻松地在 CSS 中设置它们的样式。

```css
.music-player-section{
    width: 100%;
    height: 100px;
    position: fixed;
    bottom: 0;
    left: 0;
    background: var(--alpha-color);
    backdrop-filter: blur(50px);
    transition: 1s;
}

.music-seek-bar{
    -webkit-appearance: none;
    width: 100%;
    position: absolute;
    top: -4px;
    height: 8px;
    background: var(--secondary-color);
    overflow: hidden;
}

.music-seek-bar::-webkit-slider-thumb{
    -webkit-appearance: none;
    height: 10px;
    width: 5px;
    background: var(--primary-color);
    cursor: pointer;
    box-shadow: -400px 0 0 400px var(--primary-color);
}

.current-song-name{
    font-weight: 300;
    font-size: 20px;
    text-align: center;
    margin-top: 5px;
    text-transform: capitalize;
}

.controls{
    position: relative;
    width: 80%;
    margin: auto;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 60px;
    font-size: 30px;
}

.controls span{
    display: none;
    opacity: 0;
    transition: 1s;
}

.music-player-section.active .controls{
    justify-content: space-between;
}

.music-player-section.active .controls span{
    font-size: 25px;
    display: block;
    opacity: 0.5;
}

.music-player-section.active .controls span.active{
    color: var(--primary-color);
    opacity: 1;
}

.controls .main i{
    margin: 0 5px;
    display: none;
}

.controls .main i.active{
    display: inline;
}
```
现在让我们创建最大化视图的样式。

```css
.music-player-section .hide{
    display: none;
    opacity: 0;
    transition: 1s;
}

.music-player-section.active .hide{
    display: block;
    opacity: 1;
}

.music-player-section.active{
    width: 100%;
    height: 100%;
    padding: 30px;
    display: flex;
    flex-direction: column;
}

.music-player-section.active .music-seek-bar{
    position: relative;
    display: block;
    border-radius: 50px;
    margin: auto;
}

.music-player-section.active .current-song-name{
    font-size: 40px;
}

.music-player-section.active .controls{
    width: 100%;
    font-size: 50px;
}

.artist-name{
    text-align: center;
    font-size: 20px;
    text-transform: capitalize;
}

.cover{
    width: 30vh;
    height: 30vh;
    object-fit: cover;
    margin: auto;
    border-radius: 20px;
    box-shadow: var(--shadow);
}

.current-time{
    position: absolute;
    margin-top: 5px;
    left: 30px;
}

.duration{
    position: absolute;
    margin-top: 5px;
    right: 30px;
}

.icon{
    position: absolute;
    top: 60px;
    transform: scale(1.3);
}

.back-btn{
    left: 40px;
}

.nav-btn{
    right: 40px;
}

/* volume button */

.volume-slider{
    -webkit-appearance: none;
    width: 100px;
    height: 40px;
    position: absolute;
    right: -35px;
    bottom: 80px;
    transform: rotate(-90deg);
    border-radius: 20px;
    background: var(--alpha-color);
    overflow: hidden;
    opacity: 0;
    display: none;
}

.volume-slider.active{
    opacity: 1;
    display: block;
}

.volume-slider::-webkit-slider-thumb{
    -webkit-appearance: none;
    height: 40px;
    width: 10px;
    background: var(--primary-color);
    box-shadow: -200px 0 1px 200px var(--primary-color);
}
```
**输出**
![在这里插入图片描述](https://img-blog.csdnimg.cn/818f96398ceb4409bc6341aecfeab838.png =400x)
并检查这些样式，现在像这样将`active`添加到 class `music-player-section` 中去。

```html
<section class="music-player-section active">
...
</section>
```
**输出**
![在这里插入图片描述](https://img-blog.csdnimg.cn/198adaf9122e422389d2222e586c20a2.png =300x)
我们最终会让这个播放器发挥作用。现在从player section类删除这个active。让我们创建播放列表部分。

## 🏆 playlist-section 播放列表部分 

```html
<section class="playlist active">

    <img src="assets/images/back.png" class="back-btn icon" alt="">

    <h1 class="title">播放列表</h1>

    <div class="queue active">
        <div class="queue-cover">
            <img src="assets/images/cover 1.png" alt="">
            <i class="fas fa-pause"></i>
        </div>
        <p class="name">song 1</p>
    </div>
    // +7
</section>
```
**CSS**

```css
.playlist{
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    right: -100%;
    padding: 30px 0;
    background: var(--background);
    z-index: 3;
    transition: 1s;
    overflow: auto;
}

.playlist.active{
    right: 0;
}

.title{
    font-weight: 300;
    font-size: 40px;
    text-align: center;
    margin-top: 15px;
    text-transform: capitalize;
    margin-bottom: 30px;
}

.queue{
    width: 100%;
    height: 80px;
    padding: 0 30px;
    display: flex;
    align-items: center;
    border-top: 2px solid var(--alpha-color);
}

.queue-cover{
    width: 60px;
    height: 60px;
    border-radius: 10px;
    overflow: hidden;
    margin-right: 20px;
    position: relative;
}

.queue-cover img{
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.queue-cover i{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 30px;
    color: var(--primary-color);
    display: none;
}

.queue.active i{
    display: block;
}

.queue .name{
    font-size: 22px;
    text-transform: capitalize;
}
```
**输出**

![在这里插入图片描述](https://img-blog.csdnimg.cn/34a1c4fff7174412ad1b83d3648692f1.png =200x)
我们已经完成了所有的造型。active也从播放列表部分删除类。

现在让我们 JS 使这个音乐应用程序功能齐全。

## ✨ navigation 导航部分
我们的音乐播放器中有三个部分。因此，为这个应用程序设置导航系统对我们来说非常重要。通过它我们可以轻松地从一个部分导航到另一个部分。对？所以编码这个。

```javascript
/////////////////////导航////////////

////////////切换音乐播放器
const musicPlayerSection = document.querySelector('.music-player-section');
let clickCount = 1;
musicPlayerSection.addEventListener('click', () => {
    if(clickCount >= 2){
        musicPlayerSection.classList.add('active');
        clickCount = 1;
        return;
    }
    clickCount++;
    setTimeout(() => {
        clickCount = 1;
    }, 250);
})

/////// 从音乐播放器返回
const backToHomeBtn = document.querySelector('.music-player-section .back-btn');

backToHomeBtn.addEventListener('click', () => {
    musicPlayerSection.classList.remove('active');
})

/////// 访问播放列表
const playlistSection = document.querySelector('.playlist');
const navBtn = document.querySelector('.music-player-section .nav-btn');

navBtn.addEventListener('click', () => {
    playlistSection.classList.add('active');
})
////////// 从播放列表返回到音乐播放器
const backToMusicPlayer = document.querySelector('.playlist .back-btn');

backToMusicPlayer.addEventListener('click', () => {
    playlistSection.classList.remove('active');
})
//////导航完成////////////////
```
这是基本的 JS，我还在代码中添加了注释。因此，如果您对此代码有任何疑问，请随时在讨论中问我。我们的导航完成了。所以让我们创建我们的音乐播放器。

## 🎶 music 音乐部分
对于音乐播放器，我们的页面中需要一个音频源，但现在我们没有。为此在 `index.html` 中创建一个音频元素。在 body 标记的开头创建此元素。

```html
<audio src="" id="audio-source"></audio>
```
现在我们必须创建很多函数，所以在开始之前让我们快速选择我们可能需要进行操作的所有元素。

```javascript
/////// 音乐

let currentMusic = 0;

const music = document.querySelector('#audio-source');

const seekBar = document.querySelector('.music-seek-bar');
const songName = document.querySelector('.current-song-name');
const artistName = document.querySelector('.artist-name');
const coverImage = document.querySelector('.cover');
const currentMusicTime = document.querySelector('.current-time');
const musicDuration = document.querySelector('.duration');

const queue = [...document.querySelectorAll('.queue')];

// 在此处选择所有按钮

const forwardBtn = document.querySelector('i.fa-forward');
const backwardBtn = document.querySelector('i.fa-backward');
const playBtn = document.querySelector('i.fa-play');
const pauseBtn = document.querySelector('i.fa-pause');
const repeatBtn = document.querySelector('span.fa-redo');
const volumeBtn = document.querySelector('span.fa-volume-up');
const volumeSlider = document.querySelector('.volume-slider');
```
现在设置音乐源。

```javascript
// 音乐设置功能

const setMusic = (i) => {
    seekBar.value = 0;
    let song = songs[i];
    currentMusic = i;

    music.src = song.path;

    songName.innerHTML = song.name;
    artistName.innerHTML = song.artist;
    coverImage.src = song.cover;

    setTimeout(() => {
        seekBar.max = music.duration;
        musicDuration.innerHTML = formatTime(music.duration);
    }, 300);
    currentMusicTime.innerHTML = '00 : 00';
    queue.forEach(item => item.classList.remove('active'));
    queue[currentMusic].classList.add('active');
}

setMusic(0);
```
你可以注意到，为了设置持续时间，我们调用了formatTime，现在创建这个。

```javascript
// 格式持续时间为 00 : 00 格式

const formatTime = (time) => {
    let min = Math.floor(time / 60);
    if(min < 10){
        min = `0` + min;
    }

    let sec = Math.floor(time % 60);
    if(sec < 10){
        sec = `0` + sec;
    }

    return `${min} : ${sec}`;
}
```
现在让我们添加播放/暂停事件。

```javascript
// playBtn 点击事件

playBtn.addEventListener('click', () => {
    music.play();
    playBtn.classList.remove('active');
    pauseBtn.classList.add('active');
})

// pauseBtn 点击事件

pauseBtn.addEventListener('click', () => {
    music.pause();
    pauseBtn.classList.remove('active');
    playBtn.classList.add('active');
})
```
我们已经完成了音乐的设置和播放/暂停。现在进行向前/向后事件。

```javascript
//  向前按钮

forwardBtn.addEventListener('click', () => {
    if(currentMusic >= songs.length - 1){
        currentMusic = 0;
    } else{
        currentMusic++;
    }
    setMusic(currentMusic);
    playBtn.click();
})

// 后退按钮

backwardBtn.addEventListener('click', () => {
    if(currentMusic <= 0){
        currentMusic = songs.length - 1;
    } else{
        currentMusic--;
    }
    setMusic(currentMusic);
    playBtn.click();
})
```
快完成了，现在创建搜索栏功能。

```javascript
// 搜索栏事件

setInterval(() => {
    seekBar.value = music.currentTime;
    currentMusicTime.innerHTML = formatTime(music.currentTime);
    if(Math.floor(music.currentTime) == Math.floor(seekBar.max)){
        if(repeatBtn.className.includes('active')){
            setMusic(currentMusic);
            playBtn.click();
        } else{
            forwardBtn.click();
        }
    }
}, 500)

seekBar.addEventListener('change', () => {
    music.currentTime = seekBar.value;
})
```
做了这个之后。创建刷新功能和音量选项。

```javascript
// 刷新按钮

repeatBtn.addEventListener('click', () => {
    repeatBtn.classList.toggle('active');
})

// 音量部分

volumeBtn.addEventListener('click', () => {
    volumeBtn.classList.toggle('active');
    volumeSlider.classList.toggle('active');
})

volumeSlider.addEventListener('input', () => {
    music.volume = volumeSlider.value;
})
```
我们的播放器完成了。我们要做的最后一件事是使我们的播放列表正常运行。

```javascript
queue.forEach((item, i) => {
    item.addEventListener('click', () => {
        setMusic(i);
        playBtn.click();
    })
})
```

到这里我们已经完成了所有代码。播放器、导航栏、播放列表、轮播图，刷新，音量加减等等

## 🛬 wuhu ! 起飞 !

希望通过本文，您已经学会了如何使用 HTML、CSS 和 JS 的在线音乐播放器。我之前使用 HTML、CSS 和 JavaScript 制作了更多类型的小工具，如果您愿意，可以查看这些设计。

[使用 HTML、CSS 和 JS 的简单倒数计时器](https://haiyong.blog.csdn.net/article/details/120203399)
[使用 HTML、CSS 和 JavaScript 制作的随机密码生成器](https://haiyong.blog.csdn.net/article/details/119407004)
[使用 HTML、CSS、JS 和 API 制作一个很棒的天气 Web 应用程序](https://haiyong.blog.csdn.net/article/details/119079126)
[你真的熟练运用 HTML5 了吗，这10 个酷炫的 H5 特性你会几个？](https://haiyong.blog.csdn.net/article/details/118487938)
[使用 HTML、CSS 和 JS 创建响应式可过滤的游戏+工具展示页面 ](https://haiyong.blog.csdn.net/article/details/120085442)
[11个基于HTML/CSS/JS的情人节表白可爱小游戏、小动画【情人节主题征文】](https://haiyong.blog.csdn.net/article/details/113812064)


> 我已经写了很长一段时间的技术博客，并且主要通过CSDN发表，这是我的一篇 Web 在线音乐播放器教程。我喜欢通过文章分享技术与快乐。您可以访问我的博客： [https://haiyong.blog.csdn.net/](https://haiyong.blog.csdn.net/) 以了解更多信息。希望你们会喜欢！😊

<font color="#7FFF00">**💌 欢迎大家在评论区提出意见和建议！💌**</font>

## 🎡 完整源码下载

<font color="#F08080" id="jump99">**如果你真的从这篇文章中学到了一些新东西，喜欢它，收藏它并与你的小伙伴分享。🤗最后，不要忘了❤或📑支持一下哦。**</font>

**完整的源代码：[点击此处下载](https://download.csdn.net/download/qq_44273429/22643233)** （可能审核不过）

**免费源码可通过下方公号回复【代码】获取👇🏻👇🏻👇🏻**

<img src="https://img-blog.csdnimg.cn/07d5c80f7ae44ca7b8d441cc0c19943f.png#pic_center%E2%80%9D">
