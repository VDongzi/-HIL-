# 协作指南

`main` 分支受保护，不能直接推送。所有修改都通过「分支 → Pull Request（PR）→ 合并」完成，仓库所有者也一样。

## 首次准备

1. 安装 Git、Python 和 Chrome，以及字体 **Clash Vector、Inter、Noto Sans CJK SC**。缺少字体时文字会显示成其他字体，和导出的视频不一致。
2. 获取项目：

   ```bash
   git clone https://github.com/VDongzi/-HIL-.git
   ```

3. 在项目文件夹中启动预览：

   ```bash
   python -m http.server 8765
   ```

   然后用 Chrome 打开 http://localhost:8765/HIL%E6%B5%8B%E8%AF%95%E5%8A%A8%E7%94%BB.html 。

第一次 `git push` 时会弹出浏览器窗口，登录 GitHub 即可。

## 每次修改的流程

1. 先获取最新版本：

   ```bash
   git switch main
   git pull
   ```

2. 新建分支，用任务内容命名，例如 `fix-subtitle-wrap`：

   ```bash
   git switch -c fix-subtitle-wrap
   ```

3. 修改文件，在浏览器中按 Ctrl+F5 刷新预览。
4. 提交并推送：

   ```bash
   git add -A
   git commit -m "缩短白框页面的长字幕"
   git push -u origin fix-subtitle-wrap
   ```

5. 推送后 GitHub 页面会出现 **Compare & pull request** 按钮，点击后写明改了什么，最好附一张截图。
6. 其他人在 PR 中查看并留言。确认没问题后点击 **Merge pull request**，再删除该分支。
7. 回到本地更新：

   ```bash
   git switch main
   git pull
   git branch -d fix-subtitle-wrap
   ```

## 避免冲突

几乎所有内容都在 `HIL测试动画.html` 一个文件里，多人同时修改时最容易冲突：

- **按页面或章节分工**，避免两人同时改同一个场景。用 GitHub Issues 记录「谁在做什么」：一个任务一个 Issue，并指定负责人。
- **PR 保持小而快**，改完尽快合并。分支存在越久，和 `main` 差得越多。
- **提交 PR 前**，在自己的分支上运行 `git pull origin main` 合入最新修改，在本地解决冲突后再推送。

## 注意事项

- **旁白时间轴**：字幕和动画按照 `NARR.starts` / `NARR.ends` 中的时间点同步，对应 `assets/narration.m4a`。如果重新录制旁白或修改字幕文字，这些时间点也要一起更新。
- **颜色**：只使用代码中 `C` 常量里的品牌色。
- **字体**：标题使用 Clash Vector Medium + Noto Sans CJK SC Medium，正文使用 Inter + Noto Sans CJK SC Regular。
- **导出视频**：在装好字体的电脑上用 Camtasia 录制。最终版本由谁录制请事先约定。
