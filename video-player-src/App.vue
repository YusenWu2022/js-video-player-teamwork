<template>
	<div>
	<!--视频组件-->
	   <video-player
        class="video-player"
        ref="VideoPlayer"
        :options="playerOptions"
      >
      </video-player>
	</div>
</template>
<script>
import { VideoPlayer } from "vue-video-player";
export default {
  name: "newStaffMediaPlay",
  // 添加组件
  components: {
    VideoPlayer,
  },
  // 定义变量
   data() {
    return {
		mediaUrl: null, // video path

    // player settings
		playerOptions: {
	        playbackRates: [1.0], // 可选的播放速度
	        autoplay: true, // 如果为true,浏览器准备好时开始回放。
	        muted: false, // 默认情况下将会消除任何音频。
	        loop: false, // 是否视频一结束就重新开始。
	        preload: "auto", // 建议浏览器在<video>加载元素后是否应该开始下载视频数据。auto浏览器选择最佳行为,立即开始加载视频（如果浏览器支持）
	        language: "zh-CN",
	        aspectRatio: "16:9", // 将播放器置于流畅模式，并在计算播放器的动态大小时使用该值。值应该代表一个比例 - 用冒号分隔的两个数字（例如"16:9"或"4:3"）
	        fluid: true, // 当true时，Video.js player将拥有流体大小。换句话说，它将按比例缩放以适应其容器。
	        sources: [
	          {
	            type: "video/mp4", // 类型
	            src: "", // url地址
	          },
	        ],
	        poster: "", // 封面地址
	        notSupportedMessage: "此视频暂无法播放，请稍后再试", // 允许覆盖Video.js无法播放媒体源时显示的默认信息。
	        controlBar: {
	          timeDivider: true, // 当前时间和持续时间的分隔符
	          durationDisplay: true, // 显示持续时间
	          remainingTimeDisplay: true, // 是否显示剩余时间功能
	          fullscreenToggle: true, // 是否显示全屏按钮
        },
      },
	}
  },
  // 方法
  methods: {
  // 获取视频路径方法
	  getMedia() {
	  // 假定此临时变量为后端获取的路径
	  	let mediaPath = "D:/EXAM_MATERIAL/NEW-STAFF/VIDEO/B-0001/1/B-0001.mp4";
	  	// 处理路径，防止出现浏览器禁止访问问题
        mediaPath = mediaPath.replace("D:/EXAM_MATERIAL", "/EXAM_MATERIAL");
        let name = mediaPath.substring(mediaPath.lastIndexOf("/") + 1);
        this.mediaUrl =
          mediaPath.substring(0, mediaPath.lastIndexOf("/") + 1) +
          encodeURI(name);
          // 在视频控件设置视频路径
        this.playerOptions.sources[0].src = this.mediaUrl;
        this.playerOptions.sources[0].src = require("./assets/src.mp4");
	  }
	},
  // created
  created() {
	// 进入页面加载获取后端传过来的视频路径进行播放
	this.getMedia();
	},
}
</script>

