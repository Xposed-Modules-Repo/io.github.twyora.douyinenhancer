# 抖柚

[![GitHub](https://img.shields.io/github/license/twyora/DouyinEnhancer)](https://github.com/twyora/DouyinEnhancer/blob/main/LICENSE)
![GitHub tag (latest by date)](https://img.shields.io/github/v/tag/twyora/DouyinEnhancer)

[English](README.md) | [简体中文](README_zh_CN.md)

为抖音添加一些优化体验的小功能

> 项目仍处于早期阶段，功能还在逐步完善中，欢迎反馈和建议

## 测试环境

> 抖音 37.6.0
---
> 其它版本未经验证，不保证功能可用性，若存在问题欢迎提交 Issue 或 PR

## 模块功能

- [x] 评论区图片无水印下载
- [x] 评论区表情包保存到相册
- [x] ~~视频过滤~~ 推荐流过滤
- [x] 播放内容保存到相册（暂不支持受限制内容下载）
- 解除受限制内容下载
- 已收藏表情保存到相册
- [x] 模块设置页面
- 清屏播放不隐藏弹幕
- [x] 缓存被混淆方法的查找结果，提升宿主启动速度
- [x] 保存评论区语音评论
- 移除听抖音版权限制
- [x] 模块设置的备份与恢复
- 模块设置页面支持深色模式
- 打开评论界面之后暂停视频
- 观看视频时禁用双击点赞行为
- 隐藏播放时叠加在视频上的特定组件（如点赞、文案描述等）
- 隐藏 TAB 栏中间的“发布按钮”
- 推荐流视频播放完毕之后自动切换下一条
- 推荐流视频播放完毕之后暂停
- 指定初始倍数播放视频
- 更加可靠的在宿主设置页注入模块设置项的方式
- [x] 添加更多模块设置入口
- 尝试适配更多新版本
- ......

## 使用方法

1. 在 Xposed 管理器（如 LSPosed）中激活模块
2. 作用域勾选抖音（`com.ss.android.ugc.aweme`）
3. 重启抖音

## 免责声明

- 本项目仅供个人学习与技术交流使用，请勿用于商业用途
- 使用本模块产生的一切后果均由使用者自行承担

## 致谢

> 排名不分先后

- [BiliRoaming](https://github.com/yujincheng08/BiliRoaming)
- [DexKit](https://github.com/LuckyPray/DexKit)
- [gif.kt](https://github.com/shaksternano/gif.kt)
- [Gropify](https://github.com/HighCapable/Gropify)
- [KavaRef](https://github.com/HighCapable/KavaRef)
- [RestoreSplashScreen](https://github.com/GSWXXN/RestoreSplashScreen)
- [YukiHookAPI](https://github.com/HighCapable/YukiHookAPI)
