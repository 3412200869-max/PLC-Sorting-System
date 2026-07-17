# PLC开发环境安装执行计划 V1.0

| 文档属性 | 内容 |
|---|---|
| 项目名称 | PLC-Sorting-System |
| 文档编号 | PSS-INST-001 |
| 文档版本 | V1.0 |
| 编制日期 | 2026-07-13 |
| 项目阶段 | 阶段3：PLC程序实现与PLCSIM仿真（实施准备） |
| 软件基线 | TIA Portal V20 |
| 当前状态 | 执行计划已建立，安装尚未开始 |

## 1. 文档目的

本文件将阶段3开发环境准备要求转化为可执行的安装工单，明确 TIA Portal V20、STEP 7、S7-PLCSIM 和 WinCC 的版本组合、D盘目录、安装顺序、重启节点、验证步骤、证据和异常处理原则。

本次只生成安装执行计划，不安装软件、不创建正式TIA Portal工程、不生成PLC代码。

## 2. 适用范围

### 2.1 本次计划包含

- 安装前电脑、操作系统、磁盘、权限和许可证检查。
- TIA Portal V20基础环境。
- STEP 7 Basic V20；学校提供Professional许可时可改为Professional V20。
- S7-PLCSIM V20标准版。
- WinCC Advanced V20及需要的Runtime Advanced/仿真组件。
- Automation License Manager和官方兼容更新。
- 安装后的软件启动、虚拟CPU、空项目编译、PLCSIM和WinCC环境验证。

### 2.2 本次计划不包含

- PLC-Sorting-System正式TIA工程创建。
- PLC标签、DB、OB、FB、FC和控制逻辑编写。
- WinCC正式画面组态。
- PLCSIM正式物料模型和故障场景实现。
- 非官方安装包、破解软件、许可证绕过或系统兼容性绕过。

## 3. 软件安装基线

| 序号 | 软件/组件 | 计划版本 | 计划选项 | 说明 |
|---:|---|---|---|---|
| SW-01 | TIA Portal | V20 | 基础工程环境 | 统一管理PLC、HMI、网络、编译和归档 |
| SW-02 | STEP 7 | Basic V20 | S7-1200工程功能 | 本项目不需要S7-1500高级功能；有学校Professional许可时可使用Professional V20 |
| SW-03 | S7-PLCSIM | V20 Standard | 单虚拟S7-1200 CPU | 不安装PLCSIM Advanced，除非后续另行批准 |
| SW-04 | WinCC | Advanced V20 | Engineering + Runtime Advanced/仿真 | 学校若统一使用Unified，必须重新评审并整套切换，不在本计划中混装 |
| SW-05 | Automation License Manager | 与V20介质配套 | 官方默认版本 | 管理STEP 7、WinCC和Runtime许可证 |
| SW-06 | 官方Updates/HSP | V20兼容版本 | 按需安装 | 更新级别必须经过Compatibility Tool核对 |

### 3.1 基线规则

- TIA Portal、STEP 7、S7-PLCSIM和WinCC保持V20同一主版本。
- Update级别以安装时西门子官方兼容矩阵为准，不凭经验混装。
- CPU暂按S7-1200 CPU 1214C级别验证，具体订货号和固件在安装后锁定。
- 如学校实际使用V21、V19或V18，应先暂停本计划并发布修订版，不直接局部替换组件。

## 4. D盘路径规划

### 4.1 路径总表

| 用途 | 计划路径 | 是否纳入Git | 说明 |
|---|---|---|---|
| 官方安装介质 | `D:\Siemens_Installers\TIA_V20\` | 否 | 保存原始镜像、安装包和官方更新 |
| 解压/挂载工作目录 | `D:\Siemens_Installers\TIA_V20\Working\` | 否 | 仅在官方安装说明允许解压时使用 |
| 安装日志备份 | `D:\Siemens_Installers\TIA_V20\Logs\` | 否 | 复制安装结果和错误日志，不含许可证敏感信息 |
| 活动TIA工作区 | `D:\Siemens_Workspace\PLC-Sorting-System\Active\` | 否 | 阶段3正式建项后使用，避免直接在Git目录中运行活跃二进制工程 |
| 临时验证项目 | `D:\Siemens_Workspace\ENV_Verification\` | 否 | 只验证安装链路，验证后可归档记录并删除项目 |
| 临时导出目录 | `D:\Siemens_Workspace\Exports\` | 否 | 导出源、标签和编译报告的中转目录 |
| 本地Git仓库 | `D:\Automation_Project\PLC-Sorting-System\` | 是 | 已存在的项目仓库 |
| TIA受控归档 | `D:\Automation_Project\PLC-Sorting-System\PLC\tia-portal\archives\` | 是/LFS待评审 | 正式工程建立后保存阶段性归档，不在本次创建 |
| PLC文本导出 | `D:\Automation_Project\PLC-Sorting-System\PLC\tia-portal\exported-sources\` | 是 | 正式工程建立后保存可审查导出，不在本次创建 |
| PLCSIM证据 | `D:\Automation_Project\PLC-Sorting-System\Simulation\plcsim\evidence\` | 是 | 阶段3仿真开始后使用，不在本次创建 |

### 4.2 软件程序安装路径原则

目标是尽可能将允许选择的程序组件安装到D盘，例如：

```text
D:\Siemens\Automation\
```

但必须遵守以下规则：

- 只有安装器明确提供目标路径选择时，才选择D盘。
- Windows共享组件、SQL组件、Automation License Manager、驱动、服务、公共数据或西门子共享目录可能仍安装到系统盘；接受官方安装器决定。
- 不使用目录联接、符号链接、注册表强改或安装后手工移动程序文件来强制全部迁移到D盘。
- 安装前必须保证C盘仍有安装器要求的空间，因为缓存、临时文件和共享组件可能使用系统盘。
- 实际安装路径在执行记录中填写，不以计划路径替代真实结果。

### 4.3 磁盘空间门禁

- [ ] C盘可用空间大于安装器显示的系统盘需求，并额外保留安全余量。
- [ ] D盘可用空间大于所选组件、安装介质、更新包、活动工程和归档总需求，并保留安全余量。
- [ ] C盘和D盘文件系统健康，无待处理磁盘错误。
- [ ] 安装过程不使用移动硬盘、网络映射盘或云同步目录作为程序安装目标。

不在计划中写死未经官方确认的最低容量；以V20安装器和官方系统要求显示值为准，并在其基础上保留至少20%的工程余量。

## 5. 安装前检查清单

### 5.1 操作系统与电脑

- [ ] 记录Windows版本、Edition、Build和64位系统信息。
- [ ] 使用Siemens Compatibility Tool确认Windows与TIA Portal V20、PLCSIM V20、WinCC V20兼容。
- [ ] 对照V20官方系统要求检查CPU、内存、磁盘和显示分辨率。
- [ ] 电脑连接可靠电源，安装期间不进入睡眠或自动关机。
- [ ] 当前用户具有本机管理员权限。
- [ ] 完成重要数据备份，并记录系统恢复方式或恢复点。
- [ ] 完成必要的Windows更新并重启。
- [ ] Windows没有挂起的重启、更新或其他软件安装任务。
- [ ] 关闭VS Code、Office、数据库工具和其他不必要应用。
- [ ] 不永久关闭安全软件；如安全策略阻止官方安装器，按学校/系统管理规则处理并记录。

### 5.2 现有西门子软件

- [ ] 在“已安装的应用”中记录所有Siemens、TIA、WinCC、PLCSIM和Automation License Manager组件。
- [ ] 记录现有主版本、Update、Hotfix和许可证。
- [ ] 核对V20与现有版本的官方并行安装支持。
- [ ] 如需卸载冲突版本，先备份许可证和现有工程，并单独批准卸载步骤。
- [ ] 确认没有正在运行的Siemens服务或Runtime工程。

### 5.3 安装介质

- [ ] 安装包来自Siemens官方或学校授权渠道。
- [ ] 安装介质明确标识V20和具体Update。
- [ ] STEP 7、WinCC和PLCSIM介质彼此匹配。
- [ ] 如官方提供SHA校验值，完成完整性验证。
- [ ] 将介质保存至`D:\Siemens_Installers\TIA_V20\`。
- [ ] 不从压缩包内部直接运行安装程序；按官方说明挂载或完整解压后运行。

### 5.4 许可证

- [ ] 明确STEP 7 Basic/Professional许可证类型。
- [ ] 明确WinCC Advanced Engineering和Runtime许可证。
- [ ] 明确正式、教育或官方试用许可及有效期。
- [ ] 确认Automation License Manager能够管理该许可证。
- [ ] 许可证文件、序列号、账号和授权截图不进入Git。

### 5.5 项目保护

- [ ] 本地Git仓库`D:\Automation_Project\PLC-Sorting-System\`状态已备份或同步。
- [ ] 安装过程不修改现有项目文档。
- [ ] 临时验证项目使用独立目录，不放入Git仓库。
- [ ] 当前明确禁止开始PLC控制逻辑编写。

## 6. 安装执行顺序

### 6.1 执行状态定义

| 状态 | 含义 |
|---|---|
| Not Started | 尚未执行 |
| In Progress | 正在执行，尚未验证 |
| Pass | 安装或验证成功 |
| Fail | 执行失败，需要处理后重试 |
| Blocked | 因版本、权限、许可或兼容性无法继续 |

### 6.2 总体顺序

```text
冻结版本与路径
  → Windows/磁盘/权限检查
  → 安装TIA Portal V20基础环境
  → 安装STEP 7 Basic V20
  → 安装WinCC Advanced V20 Engineering
  → 重启
  → 安装S7-PLCSIM V20 Standard
  → 安装WinCC Runtime Advanced/仿真组件（如独立安装）
  → 重启
  → 安装官方兼容Update/HSP
  → 配置并检查许可证
  → 完成环境验证
  → 冻结环境基线
```

TIA Portal、STEP 7和WinCC Engineering可能由同一安装程序一次选择。即便在一次安装中完成，执行记录仍按组件分别确认结果。

### 6.3 详细执行工单

| 步骤 | 操作 | 目标/选择 | 重启 | 预期结果 | 初始状态 |
|---:|---|---|---|---|---|
| 01 | 填写版本、Update、WinCC产品线和许可证 | V20整套基线 | 否 | 版本方案无“待定” | Not Started |
| 02 | 建立安装介质与日志目录 | `D:\Siemens_Installers\TIA_V20\` | 否 | 介质与日志位置明确 | Not Started |
| 03 | 完成Windows、磁盘、权限和冲突检查 | 按第5章 | 是，如有更新 | 所有P0检查通过 | Not Started |
| 04 | 启动官方TIA V20安装器 | 管理员权限、官方介质 | 否 | 安装器正常运行 | Not Started |
| 05 | 选择TIA Portal基础组件 | V20 | 按提示 | TIA基础环境安装成功 | Not Started |
| 06 | 选择STEP 7 | Basic V20或已批准Professional V20 | 按提示 | S7-1200工程组件安装成功 | Not Started |
| 07 | 选择WinCC Engineering | Advanced V20 | 按提示 | HMI工程组件安装成功 | Not Started |
| 08 | 完成套件安装并保存日志 | 日志复制到D盘Logs | 是 | 重启后TIA可启动 | Not Started |
| 09 | 安装S7-PLCSIM | V20 Standard | 是 | PLCSIM可启动/被TIA调用 | Not Started |
| 10 | 安装WinCC Runtime/仿真 | Runtime Advanced V20，如未随套件安装 | 按提示 | Runtime/Simulation组件可用 | Not Started |
| 11 | 安装兼容官方Update | 与所有V20组件匹配 | 是 | 版本/Update一致且可启动 | Not Started |
| 12 | 按需安装HSP | 仅目标CPU/固件目录缺失时 | 按提示 | 目标CPU可在硬件目录选择 | Not Started |
| 13 | 检查Automation License Manager | 官方配套版本 | 否 | 许可证管理器正常 | Not Started |
| 14 | 导入/激活合法许可证 | STEP 7、WinCC、Runtime | 否 | 所需许可证有效 | Not Started |
| 15 | 执行第7章环境验证 | 临时ENV_Verification项目 | 是，验证后 | 编译、下载、在线、HMI启动均通过 | Not Started |
| 16 | 填写环境基线并归档证据 | 项目文档与D盘日志 | 否 | 阶段3环境门禁关闭 | Not Started |

## 7. 安装后验证计划

### 7.1 软件启动与版本

- [ ] TIA Portal V20正常启动。
- [ ] “帮助/关于”中的完整版本和Update已记录。
- [ ] STEP 7能够进入S7-1200硬件组态。
- [ ] S7-PLCSIM V20能够启动。
- [ ] WinCC Advanced Engineering能够打开。
- [ ] WinCC Runtime/Simulation能够启动。
- [ ] Automation License Manager显示需要的许可证有效。

### 7.2 临时空项目验证

使用`D:\Siemens_Workspace\ENV_Verification\`创建一次性项目，仅验证软件链路：

1. 新建`ENV_Verification`临时项目。
2. 添加候选S7-1200 CPU 1214C和计划固件。
3. 不编写业务逻辑，保留空程序结构。
4. 执行PLC全量编译。
5. 启动S7-PLCSIM并创建虚拟CPU。
6. 下载空项目，切换虚拟CPU到RUN。
7. 验证在线连接、离线/在线比较、RUN和STOP。
8. 添加临时WinCC对象并建立到虚拟CPU的连接。
9. 只使用内部变量或非控制测试状态验证WinCC编译和Runtime启动。
10. 关闭临时项目，记录结果；不将该项目提交到Git。

### 7.3 I/O与CPU基线验证

- [ ] 记录CPU完整名称、订货号和固件版本。
- [ ] 核对集成DI/DO数量和电气类型。
- [ ] 复核`I0.0～I1.5`共14DI的地址规划。
- [ ] 复核`Q0.0～Q0.5`共6DO的地址规划。
- [ ] 如地址不同，只修订I/O映射和点表，不修改符号接口和架构。
- [ ] 保存硬件设备视图和地址截图，遮盖个人或许可证信息。

### 7.4 重启复验

- [ ] Windows重启后TIA Portal可正常启动。
- [ ] PLCSIM虚拟CPU可重新创建并下载。
- [ ] WinCC Engineering和Runtime可正常启动。
- [ ] 许可证重启后仍有效。
- [ ] D盘工作区和Git仓库路径可正常访问。

## 8. 执行证据与记录

| 证据编号 | 内容 | 保存位置 | 是否入Git |
|---:|---|---|---|
| E-01 | 安装介质版本和校验记录 | `D:\Siemens_Installers\TIA_V20\Logs\` | 仅无敏感摘要入Git |
| E-02 | 安装成功/失败日志 | 同上 | 错误摘要可入Git，原始日志先检查敏感信息 |
| E-03 | TIA/STEP 7/PLCSIM/WinCC版本截图 | 项目文档证据目录，后续创建 | 是，脱敏后 |
| E-04 | CPU/固件与I/O地址截图 | 项目文档证据目录 | 是，脱敏后 |
| E-05 | 临时项目编译结果 | D盘Logs与项目环境记录 | 编译摘要入Git |
| E-06 | PLCSIM下载、RUN、STOP证据 | D盘Logs与后续Simulation证据目录 | 是，脱敏后 |
| E-07 | WinCC编译与Runtime启动证据 | D盘Logs与后续HMI证据目录 | 是，脱敏后 |
| E-08 | 许可证状态 | 仅记录类型、有效/无效和到期日 | 禁止提交许可证详情 |

## 9. 安装异常处理

### 9.1 停止条件

出现以下任一情况立即停止后续步骤：

- Compatibility Tool显示目标组合不受支持。
- 安装包来源或完整性无法确认。
- 系统盘或D盘空间低于安装器需求。
- 安装器要求卸载现有软件但尚未完成工程/许可证备份。
- STEP 7、WinCC或Runtime没有合法可用许可证。
- 安装后重启出现系统异常、服务错误或软件无法启动。

### 9.2 处理原则

- 保存安装器错误码、日志、当前步骤和已安装组件清单。
- 先查西门子官方Readme、Compatibility Tool和Industry Online Support。
- 不通过修改系统检测、删除未知注册表项或使用非官方补丁绕过问题。
- 需要卸载、修复或更换版本时，先更新本计划的执行记录并确认回退方案。

## 10. 安装执行记录模板

| 字段 | 记录值 |
|---|---|
| 执行日期 | 待填写 |
| 执行人 | 待填写 |
| Windows版本/Build | 待填写 |
| TIA Portal V20 Update | 待填写 |
| STEP 7 Edition/Update | 待填写 |
| S7-PLCSIM Update | 待填写 |
| WinCC产品/Update | 待填写 |
| Runtime产品/版本 | 待填写 |
| Automation License Manager | 待填写 |
| 许可证类型/到期日 | 待填写，不写敏感信息 |
| 实际程序安装路径 | 待填写 |
| D盘介质目录 | 待填写 |
| D盘活动工作区 | 待填写 |
| CPU订货号/固件 | 待填写 |
| DI/DO地址验证 | 待填写 |
| 临时项目验证结果 | Not Started |
| WinCC验证结果 | Not Started |
| 最终结论 | Not Started |

## 11. 完成标准

- [ ] 所有安装前P0检查通过。
- [ ] TIA Portal V20、STEP 7 V20、S7-PLCSIM V20、WinCC V20版本兼容。
- [ ] 所需许可证有效。
- [ ] 临时S7-1200项目编译、下载、RUN、STOP和在线监视通过。
- [ ] WinCC Engineering与Runtime/仿真验证通过或有已批准替代方案。
- [ ] CPU型号、固件、DI/DO地址完成记录。
- [ ] Windows重启后复验通过。
- [ ] 环境基线和证据完成归档。
- [ ] 未在本安装任务中生成PLC控制逻辑。

## 12. 下一任务

安装和验证全部通过后，下一任务为 **创建PLC-Sorting-System正式TIA Portal工程骨架**。该任务仅建立CPU、网络、PLC标签表和DB结构并执行编译，不应直接跳过模块化实施步骤编写完整控制程序。

## 13. 官方核对入口

- [Siemens TIA Portal产品信息](https://www.siemens.com/global/en/products/automation/industry-software/automation-software/tia-portal.html)
- [Siemens Industry Online Support](https://support.industry.siemens.com/)
- [Siemens Compatibility Tool](https://support.industry.siemens.com/compatool/)

正式执行前必须重新核对V20官方Readme、系统要求、兼容矩阵和学校许可证条件。

## 14. 变更记录

| 版本 | 日期 | 内容 |
|---|---|---|
| V1.0 | 2026-07-13 | 建立TIA Portal V20安装顺序、D盘路径、前置检查和验证执行计划 |
