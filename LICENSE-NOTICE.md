# LICENSE-NOTICE — 许可分层与仓库边界

> **本文件是说明性 NOTICE，不是正式 EULA，也不是许可合同。**
> 正式条款以 ZNGL 的 `LICENSE`、法务核定的 EULA 增补条款与商业合同为准。
> 本文件不能替代、也不能修改正式条款；如与正式条款冲突，以正式条款为准。

本仓库只包含三个低层 API 示例页、README、本 NOTICE、`.gitignore` 和截图。
它**不包含** ZNGL `dist`、Engine 源码、许可校验逻辑、私钥/签名材料或客户数据。

---

## 1. 分层口径（摘自 `README-LICENSE-TIERS.md`）

ZNGL 自 1.1.0 起分两层：**低层 API 免费，Engine 收费**。两层说的是“要不要许可”，
不是“能不能用”。

### 1.1 免费层：低层 API（无需许可）

以下接口不需要许可文件，也不需要 `__ZNGL_LICENSE__` / `__ZNGL_HOST__`：

- `createWebGL2Context`、`Renderer`、`Scene`、`Geometry`、`Material`、`Lighting`、`OrbitCamera`；
- `uploadGeometry` / `reuploadAll` / `serializeScene` / `deserializeScene`；
- `Ray` / `raycast` / `pickScene` / `rayFromCamera` / `rayFromScreen`；
- 数学、包围盒、动画与工具模块（`Vec3` / `Mat4` / `Quat` / `Box3` / `AnimationMixer` 等）。

可以用于集成、演示、教学、评估；**商用建议允许**（正式授权以 EULA 增补条款为准）。
条件是：保留版权与版本标识；不改包绕过许可；不单独再分发 `dist`；不去水印/去标识。

### 1.2 商业层：Engine（需许可，fail-closed）

`new ZNGL.Engine(canvas)` 在创建任何 WebGL 资源**之前**校验许可；无有效许可直接抛错，
不静默放行。本仓库**没有使用 Engine**，也没有复制或实现任何许可校验。

---

## 2. 本示例仓库的边界

- 三个页面只调用低层符号，**没有 `new ZNGL.Engine(...)`**；
- 没有设置或读取 `__ZNGL_LICENSE__` / `__ZNGL_HOST__`；
- 没有 Ed25519 校验代码、公钥/私钥、许可文件或签名材料；
- 没有 `dist`；运行时需要的 `dist/zngl.js` 由使用者从正式发布包自行放入 `dist/`；
- `.gitignore` 忽略 `dist/`、`*.zip` 和系统临时文件，避免误提交；
- 页面里的 “Engine”“许可” 字样只出现在说明文字中，用于解释边界。

因此，**示例不含 Engine / 许可逻辑**；它只演示低层 API 的调用方式。

---

## 3. 允许与禁止（摘要）

允许：

- 阅读、修改这些示例页，用于对接/评估 ZNGL 低层 API；
- 随自己的产品/项目嵌入低层 API（嵌入分发按正式 EULA 处理）；
- 保留本 NOTICE 与 README 的许可分层说明。

禁止（违反即违约，具体以正式条款为准）：

1. 改包、打补丁、替换常量等方式绕过或禁用 Engine 许可校验；
2. 剥离、删除、隐藏许可逻辑或许可文件校验；
3. 去除、遮盖、篡改版权、商标、版本号、水印或“商业版”标识；
4. 单独再分发 `dist`、开发包、源码、许可文件或签名材料（随自有产品嵌入式分发除外）；
5. 把“低层免费”说成“Engine 免费”，或以官方名义为改包版本背书。

`dist` 不在本仓库中，正是为了避免第 4 条被无意触发。

---

## 4. 这不是“防破解”

JS 单文件无法防破解；公开分析已证明改一行常量即可绕过 Engine 构造校验。ZNGL 不承诺、
也不宣传“防破解/无法破解”。这套机制的定位是**合规校验**：Ed25519 签名 → 到期 →
机器绑定 → Engine fail-closed；安全边界靠合同、服务与商业条款，不靠 `dist`。

---

## 5. 来源与版本

| 项 | 内容 |
|---|---|
| 许可分层依据 | `README-LICENSE-TIERS.md`（T-0708）与 `607-ZNGL许可边界.md`；均为内部文档，不随本仓库分发 |
| 验证所用运行时 | ZNGL 1.1.0（r5）`dist/zngl.js`，444,069 字节，SHA256 `84D4435141A8D0BA32E3629984A2E085B71819645CEE113CD0A5649F6FB7C504` |
| 示例代码 | 纯 HTML/JS 示例，无独立开源许可文本；如需再分发示例代码，请先与权利方确认 |

`README-LICENSE-TIERS.md` 与 EULA 增补条款仍在法务核定流程中；本 NOTICE 中带
“建议/以正式条款为准”的表述不构成对客户的承诺。

---

## 6. 免责

示例按“现状”提供，不承诺适销性、特定用途适用性或无错误。示例中的尺寸、相机参数与
显示模式仅用于演示；接入产品前请自行做功能、性能与许可合规评审。
