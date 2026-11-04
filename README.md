# 一个医生，两种声音：研究材料包

2026 年 11 月 4 日 · 对应研究计划 v1.3 / 材料规格 v1.5

在线入口：https://lllinyan.github.io/one-physician-two-voices/

仓库：https://github.com/lllinyan/one-physician-two-voices

当前材料版本：`build-2026-11-04.1`；内容版本：`draft-2026-11-04.1`。

这是公开托管的研究预览版。病例 A、B 的正文、依据和理由已写出，临床审核状态为 pending。正式模式暂未开放。备用空腹血糖病例保留为待临床拟稿的框架。

## 从哪里打开

1. 打开本文件同目录的 **index.html**，进入研究者入口。
2. 保持「内部预览」，填写参与者编号和场次编号，选择顺序与两个方向。
3. 点击「打开模拟问诊」。依次体验 AI 回复、医生回复和七个操作入口。
4. 两个情境完成后，回到研究者入口，点击「打开设计工作台」。工作台自动使用这场的分身病例和建议方向。
5. 在工作台点击「打开展示窗口」，把这个窗口共享给参与者。研究者操作窗口保留备注、修改来源及控制项。

所有页面均为自包含 HTML。直接用桌面 Chrome 打开即可；参与者离线版本为 `M2_prototype/offline.html`。如浏览器限制本地文件或双窗，在本目录启动静态服务后打开 `http://127.0.0.1:8765/`：

```sh
python3 -m http.server 8765 --bind 127.0.0.1
```

本机地址用于本机走查。远程参与者使用经过实测的静态托管地址，或下载离线文件后在已验证设备打开。手机能否保存和交回文件，应按实际机型演练并记录。

## 包内文件

| 编号 | 文件或目录 | 用法 |
|---|---|---|
| M1 | `M1_content/content.json` | 病例、身份与设计素材文本来源 |
| M1 | `content-readable.md` / `clinical-review-table.md` | 可读材料与逐文本临床审核表 |
| M2 | `M2_prototype/online/index.html` / `offline.html` | 参与者原型；两版功能一致 |
| M3 | `M3_studio/index.html` / `display.html` | 研究者编辑窗口 / 参与者展示窗口 |
| M3 | `M3_studio/material-cards/index.html` | 28 张设计素材效果图 |
| M3 | `M3_studio/blank-templates/` | 4 张草图模板及一个 4 页 A3 打印 PDF |
| M4 | `M4_supplements/index.html` | 一致 8 张、顺序互换 8 张截图 |
| M5 | `M5_facts.md` | 主持人按当前阶段回答事实问题 |
| M6 | `M6_moderator-guide.md` | 85 分钟主持稿及分支处理 |
| M7 | `M7_recruitment-screening.md` | 招募帖、筛选表及目的性抽样记录说明 |
| M8 | `M8_consent-debrief-draft.md` | 待填写机构和实际数据路径的同意、告知草案 |
| M9 | `M9_records.xlsx` | 12 张记录表，含 16 场预分配 |
| 来源 | `wording-sources.md` | 每类措辞的设定、依据和待观察事项 |
| 索引 | `asset-manifest.json` / `allocation.json` | 图片版本索引 / 可复现的分配快照 |
| 验收 | `qa/acceptance.md` | 功能测试、独立复核和待人工落实项 |

## 一场的操作顺序

主持人按 M6 进行。原型在阶段 A 隐藏医生回复和操作区；口头完成初始理解后，提示参与者点击「查看医生回复」。意外提前点击，在研究者控制区登记。

「结束咨询」关闭当前情境的联系发送，仍可查看依据并进入下一情境。「退出本场研究」停止整场流程，主持人另行记录参与者对已有数据的保留或删除选择。

两情境完成会下载检查点，随后进行比较、真实经历和设计。工作台先留出自拟方案阶段，再按 D1、D2、D3/D3′、D4、D5、D6 固定顺序浏览。医学文字的改写另存为参与者提议，保留原文。完成方案后记录参与者确认；后续修改会要求重新确认。

收尾先完成告知，在原型研究者控制区点击「记录整场研究完成」，再导出、交回和现场打开核对。确认交回后再导出最终记录。最后按同意书清理对应设备的本场记录及下载副本。

## 数据存在哪里

页面不发起数据请求，也不调用 AI。三类记录在实际使用设备的浏览器本地保存：

- 问诊：`one-physician:session:<session_id>`。
- 工作台：`one-physician:studio:<session_id>`；展示窗口仅接收显示所需内容。
- 研究者入口人工曝光：`one-physician:researcher:<session_id>`。

刷新或重开相同场次可恢复。切换浏览器、网址或设备时，本地记录不会自动转移：先导出 JSON，再在新页面导入。问诊导入会保留已有事件编号并建立新记录段，记录切换原因和缺失范围。配置、版本或同编号事件的内容发生冲突时，需先核对原文件。

研究者入口可合并 `participant_log`、`studio_design` 和 `researcher_log`，按事件编号去重，并导出事件 JSON 与场次 CSV。导入汇总只驻留当前页面内存；原始交回文件需按 M8 约定归档。自由文字保持在 JSON 中，CSV 导出处理了可能被电子表格当作公式的文本前缀。

工作台的 PNG 是实际展示方案快照，JSON 保存配置、素材来源、修改发起者、原文与提议、修订记录、折叠状态和确认时间。选择「保存方案 PNG + JSON」后检查两份文件均已下载。

## 版本更新与正式使用

修改文本只编辑 `M1_content/content.json`，同步可读稿和审核表，并增加 `content_version` / `study_material_version`。运行以下构建，再重新生成图片和打印文件；旧版本保留在独立受控目录。

```sh
node scripts/build.mjs
```

本仓库的 HTML 构建只需要 Node。PNG/PDF 和 M9 工作簿的生成脚本保存在研究者本地完整包；更新内容时，应在完整包重新生成这些材料后同步发布。普通走查和填写记录不需要开发依赖。

正式材料开放前，补齐以下实际记录：

1. 临床审核者对 A、B 全文本和补充顺序的签审；A 两条初始路径在中国情境下是否都适用需明确结论。必要时替换病例并重做相关材料。
2. 最终两病例选择、完整试访和必要短材料检验，验证 85 分钟流程与病例理解。
3. 伦理批准及 M8 的机构、联系人、报酬执行、存储、保存期限、删除申请期限和文件交回路径。
4. 真实部署与实际设备的访问、录屏范围、恢复、下载和交回演练。

实际审核通过后，在 JSON 顶层填写 `clinical_review_status.status="approved"`、真实 `record_id`，并将最终两个病例各自状态改为 `approved`。`node scripts/build.mjs --release` 检查临床字段；正式链接使用 `mode=study`。伦理、试访与设备记录由研究者按上述清单确认后启用。

16 场预分配采用种子 20261104 的 Mulberry32 与 Fisher–Yates 打乱：每 4 场包括 S1–S4，每个顺序覆盖四种方向配对。初始链接均为预览模式；实际排期及正式链接在 M9 中登记。


## GitHub Pages 部署

仓库以 `one-physician-site.zip` 保存完整网站源码、固定材料和空白记录模板。GitHub Actions 在 main 分支更新后解压、核对 deployment-manifest.json 中的 SHA256，再发布至 GitHub Pages。下载并解压 ZIP 后，即可浏览完整目录及运行构建脚本。

PNG/PDF 和工作簿生成脚本、完整浏览器 QA 存在研究者本地完整包；解压后运行 `node scripts/build.mjs` 可重建六个 HTML 页面。研究数据保存在操作设备本地，按主持流程导出交回。
