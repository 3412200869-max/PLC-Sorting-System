# 阶段3 PLC开发环境准备清单 V1.0

| 文档属性 | 内容 |
|---|---|
| 项目名称 | PLC-Sorting-System |
| 文档编号 | PSS-ENV-001 |
| 文档版本 | V1.0 |
| 编制日期 | 2026-07-12 |
| 项目阶段 | 阶段3：PLC程序实现与PLCSIM仿真（实施准备） |
| 目标平台 | Siemens S7-1200 |
| 当前状态 | 准备清单已建立，软件安装与验证尚未执行 |

## 1. 文档目的

本文件规定 PLC-Sorting-System 进入阶段3前需要的软件、推荐版本、安装顺序、许可证检查和安装后验证流程。完成并记录本清单后，才能锁定项目的软件环境基线并创建正式 TIA Portal 工程。

本次只编制环境准备清单，不安装软件、不创建正式工程、不进行PLC程序设计。

## 2. 版本选择原则

1. TIA Portal、STEP 7、S7-PLCSIM 和 WinCC 使用同一主版本，优先保持相同更新级别。
2. 学校环境优先：如学校机房、课程资料和许可证统一使用某一版本，本项目应尽量采用相同版本。
3. 不用“最新版”替代兼容性确认；先使用 Siemens Compatibility Tool 和各组件说明核对操作系统、CPU、固件与软件组合。
4. 项目基线一旦锁定，不在实现中途随意升级主版本。必须升级时，先归档工程、创建Git分支并完成回归测试。
5. 安装包、更新包和许可证只使用学校提供或西门子官方渠道。

## 3. 推荐版本方案

### 3.1 主推荐方案

| 组件 | 推荐基线 | 推荐理由 |
|---|---|---|
| TIA Portal | V20，使用当前可获得的官方更新级别 | 功能完整、适合S7-1200教学与软件仿真；作为稳定项目基线，不追求无必要的新版本功能 |
| STEP 7 | STEP 7 Basic V20；学校有Professional许可时可用Professional V20 | S7-1200项目使用Basic即可覆盖硬件组态、LAD/SCL、OB/FB/FC/DB；Professional不改变本项目控制设计 |
| S7-PLCSIM | S7-PLCSIM V20，非Advanced版本 | 单台S7-1200虚拟CPU和I/O/程序验证使用标准PLCSIM即可，项目初版不需要PLCSIM Advanced |
| WinCC | WinCC Advanced V20 + Runtime Advanced/仿真；如学校使用Unified，则整套改为WinCC Unified V20 | Advanced路线适合传统TIA HMI与PC软件仿真；Unified应在学校课程、许可和电脑资源匹配时选择 |
| Automation License Manager | 与所选安装介质配套的官方版本 | 用于管理STEP 7、WinCC及相关许可证/试用许可 |

### 3.2 学校V21方案

如果学校明确使用 TIA Portal V21，并能提供匹配的 STEP 7、S7-PLCSIM、WinCC 和许可证，则可将整套基线升级为 V21。升级原则如下：

- TIA Portal V21。
- STEP 7 Basic/Professional V21。
- S7-PLCSIM V21。
- WinCC Advanced或Unified V21，具体产品线与学校课程一致。
- 所有组件使用官方确认的兼容更新级别。

不得使用“TIA Portal V21 + PLCSIM V20”或“STEP 7 V20 + WinCC V21”等未经官方兼容性确认的混合方案。

### 3.3 学校旧版本方案

如果学校只提供 V18 或 V19，可整套采用学校版本。本项目所需的 S7-1200、结构化程序、PLCSIM和基础HMI能力不依赖V20专属功能。与学校保持一致通常比个人单独安装更高主版本更有利于课程文件交换和教师指导。

### 3.4 最终推荐结论

**默认项目基线：TIA Portal / STEP 7 / S7-PLCSIM / WinCC V20整套同版本。**

例外条件：学校已统一V21或只能提供V18/V19时，整套切换到学校版本。最终版本必须在安装前填写到“环境基线记录”，不能继续使用“待定”。

## 4. 软件与项目部分对应关系

| 软件 | 项目用途 | 对应设计成果 | 阶段3主要输出 |
|---|---|---|---|
| TIA Portal | 统一工程平台，管理CPU、网络、PLC程序、HMI连接、编译与归档 | 总体架构、目录规划、版本规则 | TIA主工程、硬件组态、编译报告和归档包 |
| STEP 7 Basic/Professional | S7-1200硬件组态、标签、OB/FB/FC/DB及在线诊断 | I/O点表、状态机、报警、PLC结构规划 | PLC标签表、数据块、功能块、主循环和诊断接口 |
| S7-PLCSIM | 运行虚拟S7-1200、下载、在线监视、输入修改和故障场景验证 | 仿真接口、FAT规范 | 虚拟CPU、监控表、物料场景、故障注入和测试证据 |
| WinCC | 主/手动/自动/报警/参数/诊断画面，PLC变量通信和Runtime仿真 | WinCC HMI画面与变量接口设计 | HMI画面、标签、报警、权限和联合仿真 |
| Automation License Manager | 管理工程软件和Runtime许可证 | 环境门禁 | 许可证状态记录，不纳入Git |

## 5. 安装前计算机检查

### 5.1 系统与硬件

- [ ] 记录Windows版本、版本号和系统类型。
- [ ] 通过Siemens Compatibility Tool确认该Windows版本支持所选TIA/WinCC/PLCSIM组合。
- [ ] 根据所选版本官方系统要求检查CPU、内存、可用磁盘和显示分辨率。
- [ ] 确认系统盘和安装盘有足够空间用于安装、更新、TIA缓存和项目归档。
- [ ] 确认当前Windows账户具有安装所需的管理员权限。
- [ ] 完成重要文件备份，并记录系统恢复方式。
- [ ] 安装前完成必要Windows更新并重启，确保没有挂起的重启任务。
- [ ] 关闭不必要的开发和工程软件，但不以永久关闭安全软件作为常规方案。

### 5.2 安装介质与许可

- [ ] 所有安装介质来自西门子官方或学校授权渠道。
- [ ] 记录安装包名称、版本、更新级别和下载/获取日期。
- [ ] 如官方提供校验值，核对安装包完整性。
- [ ] 确认可用的是正式许可证、教育许可证还是有期限的官方试用许可。
- [ ] 确认许可证覆盖STEP 7、WinCC Engineering和需要的Runtime组件。
- [ ] 不将许可证文件、账号、序列号或学校授权信息提交到Git。

### 5.3 冲突与兼容性

- [ ] 使用Compatibility Tool检查目标软件组合。
- [ ] 检查电脑上是否已有其他TIA主版本或更新级别。
- [ ] 如需并行安装多个主版本，先核对官方并行安装支持说明。
- [ ] 检查现有PLCSIM、WinCC Runtime和Automation License Manager是否需要升级或卸载。
- [ ] 记录虚拟化、安全策略或企业/学校管理策略可能造成的限制。

## 6. 推荐安装顺序

### 步骤1：冻结环境方案

在安装前填写：

| 项目 | 最终选择 |
|---|---|
| Windows版本 | 待填写 |
| TIA Portal主版本/Update | 待填写 |
| STEP 7版本与许可类型 | 待填写 |
| S7-PLCSIM版本/Update | 待填写 |
| WinCC产品线/版本/Runtime | 待填写 |
| 安装介质来源 | 待填写 |
| 许可证类型与有效期 | 待填写 |

### 步骤2：安装TIA Portal基础环境

- 使用同一套官方安装介质启动安装。
- 保留官方推荐的默认共享组件和安装路径，除非磁盘规划有明确要求。
- 安装过程中记录所选功能和提示信息。
- 按安装程序要求重启，不跳过强制重启。

### 步骤3：安装STEP 7

- S7-1200仅需STEP 7 Basic；已有学校Professional许可时可安装Professional。
- 确认硬件配置、PLC编程语言和在线诊断组件被选中。
- 不安装本项目不需要且无许可的高级选件。

TIA Portal和STEP 7通常由同一安装介质统一选择，步骤2与步骤3可在一次安装过程中完成，但记录中仍应分别确认。

### 步骤4：安装WinCC Engineering与Runtime/仿真

- 选择WinCC Advanced或WinCC Unified，不同时为同一项目建立两套HMI技术路线。
- 确认Engineering组件和需要的软件Runtime/仿真组件。
- 记录目标画面类型、连接能力和Runtime许可状态。
- 如果许可证暂不允许Runtime，至少确认WinCC工程组件能够打开；将联合仿真标记为Blocked，不能误报通过。

### 步骤5：安装S7-PLCSIM

- 安装与TIA/STEP 7同主版本且官方兼容的S7-PLCSIM。
- 本项目先使用标准S7-PLCSIM，不安装PLCSIM Advanced，除非后续需求和许可明确要求。
- 安装完成后按提示重启。

### 步骤6：安装官方更新与硬件支持包

- 使用西门子官方更新渠道安装与当前主版本对应的更新。
- 所有组件保持兼容的更新级别。
- 只有在目标CPU/固件不在硬件目录时才安装经过确认的HSP，避免无目的堆叠支持包。
- 更新后重新记录完整版本号。

### 步骤7：配置许可证

- 打开Automation License Manager。
- 确认STEP 7、WinCC Engineering和Runtime所需许可证可见、有效且未报错。
- 记录许可证类型和到期时间，但不保存敏感许可证内容。
- 许可证不足时停止正式工程实施，先解决许可或批准替代验证方案。

## 7. 安装完成后的验证步骤

### 7.1 版本与启动验证

- [ ] TIA Portal可正常启动，无安装修复或许可证错误。
- [ ] 在“帮助/关于”或已安装软件信息中记录TIA Portal完整版本和Update。
- [ ] STEP 7组件可用，能够进入PLC硬件组态环境。
- [ ] S7-PLCSIM可独立启动或由TIA调用。
- [ ] WinCC Engineering可用，目标Runtime/仿真组件可启动。
- [ ] Automation License Manager显示预期许可证状态。

### 7.2 临时PLC环境验证

在正式仓库之外建立一个可删除的临时验证项目，仅验证软件链路，不实现分选逻辑：

1. 新建临时TIA项目，例如`ENV_Verification`。
2. 从硬件目录添加候选S7-1200 CPU 1214C及目标固件。
3. 保留系统自动生成的空程序结构，不编写业务控制逻辑。
4. 执行全量编译，记录错误和警告。
5. 启动S7-PLCSIM并创建虚拟CPU。
6. 将空验证项目下载到虚拟CPU。
7. 切换虚拟CPU到RUN并建立在线连接。
8. 验证离线/在线比较、监控和CPU启停功能。
9. 停止虚拟CPU并关闭临时项目。

通过标准：CPU可组态、编译、下载、RUN、STOP和在线监视；无阻止使用的错误。临时项目不纳入正式Git仓库。

### 7.3 I/O资源验证

- [ ] 在候选CPU设备视图中核对集成DI、DO数量和电气类型。
- [ ] 确认或修订`I0.0～I1.5`、`Q0.0～Q0.5`地址规划。
- [ ] 如集成通道不足，记录需简化的信号或扩展模块方案。
- [ ] 记录CPU完整订货号、固件版本和地址截图。
- [ ] 地址变化只更新I/O映射，不改变符号名称和核心接口。

### 7.4 PLCSIM验证

- [ ] 虚拟CPU能够由TIA启动并下载。
- [ ] 可建立监控表并观察符号变量。
- [ ] 可修改/控制允许的仿真输入而不报通信错误。
- [ ] CPU重启后按预期进入非自动运行状态。
- [ ] 记录PLCSIM完整版本、Update和验证截图。

### 7.5 WinCC验证

使用同一临时验证项目，不建立正式画面：

1. 添加与所选WinCC产品线对应的临时HMI/PC Runtime对象。
2. 建立到虚拟S7-1200的临时连接。
3. 建立一个内部测试变量或一个非控制状态变量。
4. 编译HMI，确认无阻塞错误。
5. 启动Runtime/仿真，确认画面环境可运行。
6. 如许可和产品支持，验证HMI能够读取虚拟PLC的非控制测试状态。
7. 关闭并删除临时验证项目，不将其作为正式工程提交。

通过标准：WinCC Engineering可编译，Runtime/仿真可启动；若要求联合仿真，HMI与虚拟PLC数据交换正常。

### 7.6 许可证与重启验证

- [ ] 电脑重启后再次启动TIA、PLCSIM和WinCC。
- [ ] 许可证状态重启后仍有效。
- [ ] 没有出现试用期误识别、组件缺失或版本不匹配错误。
- [ ] 记录任何许可证期限，设置到期前提醒。

## 8. 环境验收记录

| 检查项 | 预期结果 | 实际结果 | 状态 | 证据路径 |
|---|---|---|---|---|
| TIA Portal启动与版本 | 正常启动，版本已记录 | 待填写 | Not Run | 待填写 |
| STEP 7硬件组态 | 可添加S7-1200 CPU | 待填写 | Not Run | 待填写 |
| PLC全量编译 | 无阻塞错误 | 待填写 | Not Run | 待填写 |
| PLCSIM下载与RUN | 下载、RUN、STOP、在线正常 | 待填写 | Not Run | 待填写 |
| CPU/固件与I/O地址 | 已锁定并复核 | 待填写 | Not Run | 待填写 |
| WinCC Engineering | 可创建并编译临时HMI | 待填写 | Not Run | 待填写 |
| WinCC Runtime/仿真 | 可启动；需要时与PLCSIM通信 | 待填写 | Not Run | 待填写 |
| 许可证 | 组件许可有效且期限已记录 | 待填写 | Not Run | 待填写 |
| 重启复验 | 重启后全部功能仍正常 | 待填写 | Not Run | 待填写 |

状态使用`Not Run`、`Pass`、`Fail`、`Blocked`。任何P0环境项为Fail或Blocked时，不创建正式控制工程。

## 9. 环境基线记录模板

验证通过后将以下信息写入未来的`PLC/tia-portal/README.md`和项目状态记录：

```text
Environment Baseline ID:
Windows:
TIA Portal:
STEP 7 Edition / Version / Update:
S7-PLCSIM Version / Update:
WinCC Product / Version / Runtime:
Automation License Manager:
License Type / Expiry:
CPU Order Number:
CPU Firmware:
DI Start Address / Count:
DO Start Address / Count:
Verification Project Result:
Verification Date:
Evidence Location:
Approved By:
```

## 10. 常见风险与处理

| 风险 | 表现 | 处理原则 |
|---|---|---|
| 软件主版本混用 | PLCSIM无法连接、项目无法打开 | 卸载/修复不兼容组件，统一主版本后重新验证 |
| Windows不受支持 | 安装失败或运行不稳定 | 依据Compatibility Tool选择受支持系统，不绕过系统检查 |
| 许可证不足 | 工程组件或Runtime无法启动 | 使用学校许可或官方许可；记录Blocked，不使用破解软件 |
| CPU固件不在目录 | 无法添加目标CPU | 安装官方HSP或选择学校实际支持的CPU/固件 |
| 磁盘空间不足 | 安装/归档失败 | 安装前释放空间，项目与归档保留足够余量 |
| 多版本冲突 | 启动、更新或通信异常 | 先核对官方并行安装说明，必要时使用独立计算机/受支持虚拟环境 |
| WinCC路线不明确 | Advanced与Unified重复工作 | 安装前选定一条与学校课程和许可一致的路线 |

## 11. Git与安全要求

- 安装包、许可证、密钥、账号和学校授权材料不得提交到Git。
- 环境验证截图不得包含个人账号、许可证序列号或敏感路径。
- 临时`ENV_Verification`项目不提交到正式仓库。
- 正式工程创建后，记录软件版本、CPU/固件、Git提交号和TIA归档名。
- `.gitignore`应依据实际TIA版本生成的文件进行验证后再定稿。

## 12. 官方核对入口

- [Siemens TIA Portal产品信息](https://www.siemens.com/global/en/products/automation/industry-software/automation-software/tia-portal.html)
- [Siemens Industry Online Support](https://support.industry.siemens.com/)
- [Siemens Compatibility Tool](https://support.industry.siemens.com/compatool/)

安装前应以西门子官方支持页面和学校授权信息为准，再次核对系统要求、兼容性、更新和许可。

## 13. 完成判定与下一任务

### 13.1 本清单完成标准

- [ ] 最终软件主版本和WinCC产品线已批准。
- [ ] 全部软件安装完成并记录完整版本。
- [ ] 许可证有效。
- [ ] 临时S7-1200项目可编译、下载到PLCSIM并在线监视。
- [ ] WinCC Engineering及需要的Runtime/仿真验证通过。
- [ ] CPU型号、固件和I/O地址已锁定。
- [ ] 环境基线记录完成并纳入项目文档。

### 13.2 下一任务

完成本清单并关闭环境门禁后，下一任务为 **创建TIA Portal正式工程骨架**：只建立CPU、网络、PLC标签表和DB结构，再进行编译验证。未经新的实施指令，不开始分选控制逻辑编程。

## 14. 变更记录

| 版本 | 日期 | 内容 |
|---|---|---|
| V1.0 | 2026-07-12 | 建立阶段3软件版本、安装顺序、许可与验证清单 |
