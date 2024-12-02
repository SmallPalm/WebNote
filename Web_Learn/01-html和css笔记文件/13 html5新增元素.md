# video元素

#### 插入视频元素

video常见的属性

- src：URL地址 ：视频播放的地址
- width：（像素）：设置video宽度
- height：（像素）：设置video高度
- controls：boolean类型：是否显示控制栏
- autoplay：boolean类型：是否视频自动播放
- muted：boolean类型：是否静音播放
- preload：none / metadata / auto ：是否需要预加载视频
  - metadata表示预加载元数据（比如视频时长等）
- poster：URL地址：一海报帧的URL

# audio元素

#### 插入音乐元素

audio常用的属性

- src：URL地址：音频播放的URL地址
- controls：Boolean类型：是否显示控制栏
- autoplay：Boolean类型：是否音频自动播放
- muted：Boolean类型：是否静音播放
- preload：none / metadata / auto 是否需要预加载音频

# 新增全局属性 data-*

- data设置的属性可以在javascript的DOM操作中通过dataset轻松获取到
- 通常用于html和JavaScript数据之间的一个传递
- ```html
    <div class="box" data-age="18" data-name="lmy" data-title="abc">box</div>
    <script>
      const boxel = document.querySelector('.box')
      console.log(boxel.dataset);
    </script>
  ```

- 在小程序开发使用很多 在小程序中就是通过data- 来传递数据的