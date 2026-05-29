# Awesome WAM 2026

> **World Action Model · 2026 分类全索引**
> 综合 4 篇核心综述（含 WAM 首篇专门综述 2605.12090）+ 7 个 GitHub awesome 仓库
> 覆盖 200+ 篇论文，按 10 个章节组织（Cascaded/Joint WAM + Simulator + Video WM + Latent WM 等）
> PDF 版：[WAM-Models-2026.pdf](WAM-Models-2026.pdf)

📅 最后更新：2026-05-29 · ✍ 维护者：[@miracle-techlink](https://github.com/miracle-techlink) · 姐妹仓库：[awesome-vla-2026](https://github.com/miracle-techlink/awesome-vla-2026)

---

## 0. 综述与 Awesome 仓库

## 0.1 核心综述

- [World Action Models: The Next Frontier in Embodied AI (S2)](https://arxiv.org/abs/2605.12090) — **第一篇 WAM 专门综述**。正式定义"World Action Model"概念，给出 Cascaded vs Joint 二分法。
- [World Model for Robot Learning: A Comprehensive Survey (S1)](https://arxiv.org/abs/2605.00080) — 把 World Model 在机器人里的三种用法（policy / simulator / video generation）完整梳理。
- [A Comprehensive Survey on World Models for Embodied AI](https://arxiv.org/abs/2510.16732)
- [A Review of Learning-based Dynamics Models for Robotic Manipulation](https://www.science.org/doi/10.1126/scirobotics) — Science Robotics 2025

## 0.2 Awesome 仓库

- [OpenMOSS/Awesome-WAM](https://github.com/OpenMOSS/Awesome-WAM) · S2 配套，最权威
- [NTUMARS/Awesome-World-Model-for-Robotics-Policy](https://github.com/NTUMARS/Awesome-World-Model-for-Robotics-Policy) · S1 配套
- [DravenALG/awesome-vla-wam](https://github.com/DravenALG/awesome-vla-wam) · 按来源切（VideoGen / VLM / Scratch）
- [leofan90/Awesome-World-Models](https://github.com/leofan90/Awesome-World-Models)
- [knightnemo/Awesome-World-Models](https://github.com/knightnemo/Awesome-World-Models)
- [operator22th/awesome-world-models-for-robots](https://github.com/operator22th/awesome-world-models-for-robots)
- [LMD0311/Awesome-World-Model](https://github.com/LMD0311/Awesome-World-Model)

## 0.3 与 VLA 的关系（一句话）

> **WAM = VLA + 显式建模"动作如何改变世界"**。所有 WAM 砍掉未来预测头就是 VLA；所有 VLA 加上未来预测头就是 WAM。下面的分类按 S2 综述的 Cascaded/Joint 主轴展开。

---

# 1. Cascaded WAM（先生成未来，再解动作）

**核心思想：解耦——世界模型负责"画出未来会发生什么"，独立的动作 module 再从画出来的未来里反推动作。** 早期范式（2023-2024 主流），优点是模块化、可解释，缺点是两段误差会累积。

## 1.1 Explicit Pixel-Space · Learned Action Extraction

世界模型直接生成像素级未来视频，下游用一个 learned policy/decoder 从生成视频里推动作。π0.7 是 2026 H1 首批落地实体产品的 cascaded WAM 代表作。

- [UniPi](https://arxiv.org/abs/2302.00111) — 开山之作，Universal Policies via Text-Guided Video
- [VLP (Video Language Planning)](https://arxiv.org/abs/2310.10625)
- [ThisAndThat](https://arxiv.org/abs/2407.05530)
- [Gen2Act](https://arxiv.org/abs/2409.16283)
- [TesserAct](https://arxiv.org/abs/2504.20995)
- [Vidar](https://arxiv.org/abs/2507.12898)
- [RoboEnvision](https://arxiv.org/abs/2506.22007)
- [MVISTA-4D](https://arxiv.org/abs/2602.09878)
- [Say-Dream-Act](https://arxiv.org/abs/2602.10717)
- [Veo-Act](https://arxiv.org/abs/2604.04502)
- [VAG](https://arxiv.org/abs/2604.09330)
- [π0.7](https://arxiv.org/abs/2604.15483)
- [TC-IDM](https://arxiv.org/abs/2601.18323)

## 1.2 Explicit Pixel-Space · Geometric Extraction

世界模型生成视频，但下游不学动作映射，而是从视频里抽几何结构（2D flow / 3D point flow / 3D hand trajectory），再用经典控制或 IK 接到机器人——对硬件适配最友好，跨 embodiment 迁移强。

- [AVDC](https://arxiv.org/abs/2310.08576) — 视频自监督学动作
- [Im2Flow2Act](https://arxiv.org/abs/2407.15208)
- [Dreamitate](https://arxiv.org/abs/2406.16862)
- [3DFlowAction](https://arxiv.org/abs/2506.06199)
- [NovaFlow](https://arxiv.org/abs/2510.08568)
- [VidBot](https://arxiv.org/abs/2503.07135)
- [4DGen](https://arxiv.org/abs/2507.01099)
- [RIGVid](https://arxiv.org/abs/2507.00990)
- [LV-P](https://arxiv.org/abs/2512.15840)
- [Dream2Flow](https://arxiv.org/abs/2512.24766)
- [Hind4sight-Net](https://arxiv.org/abs/2008.00456) — 早期奠基

## 1.3 Implicit Planning · Latent Representation

世界模型不生成像素也不抽几何，只产出 latent 中间表示作为"计划"，下游 policy 在 latent 上规划动作。比像素生成省算力数量级。

- [ARDuP](https://arxiv.org/abs/2406.13301)
- [VPP (Video Prediction Policy)](https://arxiv.org/abs/2412.14803)
- [LaPA](https://arxiv.org/abs/2410.11758)
- [VILP](https://arxiv.org/abs/2502.01784)
- [VideoPolicy](https://arxiv.org/abs/2508.00795)
- [villa-X](https://arxiv.org/abs/2507.23682)
- [mimic-video](https://arxiv.org/abs/2512.15692)
- [S-VAM](https://arxiv.org/abs/2603.16195)
- [OmniVTA](https://arxiv.org/abs/2603.19201)
- [MWM](https://arxiv.org/abs/2604.19683)

---

# 2. Joint WAM（世界 + 动作一锅炖）

**核心思想：一个模型同时输出未来状态和动作，避免误差累积，紧耦合。** 2025 Q4 开始成为主流，2026 H1 已经基本统治 SOTA。

## 2.1 Autoregressive · Explicit Decoupled

未来状态和动作都做成 token，丢同一个 transformer 自回归生成，但未来 token 和动作 token 在序列里分开。GR-1/2/MG 是 ByteDance 这条线的代表。

- [GR-1](https://arxiv.org/abs/2312.13139)
- [GR-2](https://arxiv.org/abs/2410.06158)
- [GR-MG](https://arxiv.org/abs/2408.14368)

## 2.2 Autoregressive · Unified Discrete

把未来帧和动作完全统一到一个离散 token 空间里——彻底用 LLM 训练栈。WorldVLA / F1 / CoT-VLA 是这一支。

- [CoT-VLA](https://arxiv.org/abs/2503.22020)
- [WorldVLA](https://arxiv.org/abs/2506.21539)
- [F1](https://arxiv.org/abs/2509.06951)
- [RynnVLA-002](https://arxiv.org/abs/2511.17502)
- [MM-ACT](https://arxiv.org/abs/2512.00975)
- [FlowVLA](https://arxiv.org/abs/2508.18269)

## 2.3 Autoregressive · Predictive Latent (JEPA-style)

不预测像素 token，预测一个紧凑的 latent embedding——继承 LeCun JEPA 路线。

- [VLA-JEPA](https://arxiv.org/abs/2602.10098)
- [JEPA-VLA](https://arxiv.org/abs/2602.11832)
- [V-JEPA 2](https://arxiv.org/abs/2506.09985)
- [V-JEPA 2.1](https://arxiv.org/abs/2603.14482)
- [WoG (World Guidance)](https://arxiv.org/abs/2602.22010)
- [DIAL](https://arxiv.org/abs/2603.29844)

## 2.4 Diffusion-Based · Unified Stream · Explicit Future

未来帧 token 和动作 chunk 在同一 token stream 里 joint denoise——大厂 foundation WAM 主流选择。Cosmos Policy / DreamZero / GigaWorld-Policy / X-WAM 是 2026 重磅。

- [PAD](https://arxiv.org/abs/2411.18179)
- [UWM](https://arxiv.org/abs/2504.02792)
- [VideoVLA](https://arxiv.org/abs/2512.06963)
- [Cosmos Policy](https://arxiv.org/abs/2601.16163)
- [DreamZero](https://arxiv.org/abs/2602.15922)
- [GigaWorld-Policy](https://arxiv.org/abs/2603.17240)
- [X-WAM](https://arxiv.org/abs/2604.26694)

## 2.5 Diffusion-Based · Unified Stream · Implicit Future

未来不显式预测，但 diffusion process 内部带有 latent future 监督。

- [FLARE](https://arxiv.org/abs/2505.15659)
- [FRAPPE](https://arxiv.org/abs/2602.17259)

## 2.6 Diffusion-Based · Multi-Stream · Cross-Attention

世界和动作各走一条 diffusion 分支，通过 cross-attention 在中间层互通。

- [DUST](https://arxiv.org/abs/2510.27607)
- [UD-VLA](https://arxiv.org/abs/2511.01718)
- [Motus](https://arxiv.org/abs/2512.13030)
- [CoVAR](https://arxiv.org/abs/2512.16023)

## 2.7 Diffusion-Based · Multi-Stream · Hidden-State Coupling

两条分支通过 hidden state 在中间层硬耦合。**2026 H1 学术界最活跃的子方向**——LingBot-VA / Fast-WAM / DiT4DiT / MotuBrain 都是这条线。

- [LingBot-VA](https://arxiv.org/abs/2601.21998)
- [LDA-1B](https://arxiv.org/abs/2602.12215)
- [AdaWorldPolicy](https://arxiv.org/abs/2602.20057)
- [AIM](https://arxiv.org/abs/2604.11135)
- [DexWorldModel](https://arxiv.org/abs/2604.16484)
- [MotuBrain](https://arxiv.org/abs/2604.27792)
- [Act2Goal](https://arxiv.org/abs/2512.23541)
- [DiT4DiT](https://arxiv.org/abs/2603.10448)
- [Fast-WAM](https://arxiv.org/abs/2603.16666)
- [WAV](https://arxiv.org/abs/2604.14732)

## 2.8 Diffusion-Based · Multi-Stream · Shared Representation

两条分支共享底层 representation backbone，再分头解码。

- [UVA](https://arxiv.org/abs/2503.00200)
- [PhysGen](https://arxiv.org/abs/2603.00110)

---

# 3. WAM 按 "来源" 分类（DravenALG 视角）

S2 是按"耦合方式"切，DravenALG 提出按"WAM 怎么训出来的"切，这两个 taxonomy 互补。

## 3.1 WAM from VideoGen（视频生成模型改造）

从已有视频生成 foundation model（Cosmos、Sora-类）出发，加上动作分支微调。优点是利用了 internet-scale 视频预训练。

- [UniPi](https://arxiv.org/abs/2302.00111)
- [VLP](https://arxiv.org/abs/2310.10625)
- [GR-1](https://arxiv.org/abs/2312.13139)
- [GR-2](https://arxiv.org/abs/2410.06158)
- [VPP](https://arxiv.org/abs/2412.14803)
- [Inverse Probabilistic Adaptation](https://arxiv.org/abs/2504.15369)
- [DreamGen](https://arxiv.org/abs/2505.12705)
- [UniVLA (task-centric)](https://arxiv.org/abs/2505.06111)
- [VideoPolicy](https://arxiv.org/abs/2508.00795)
- [mimic-video](https://arxiv.org/abs/2512.15692)
- [LingBot-VA](https://arxiv.org/abs/2601.21998)
- [World-VLA-Loop](https://arxiv.org/abs/2602.06508)
- [Cosmos Policy](https://arxiv.org/abs/2601.16163)
- [DreamZero](https://arxiv.org/abs/2602.15922)
- [Do WAMs Generalize Better?](https://arxiv.org/abs/2603.22078)
- [Fast-WAM](https://arxiv.org/abs/2603.16666)
- [GigaWorld-Policy](https://arxiv.org/abs/2603.17240)

## 3.2 WAM from VLM（视觉语言模型改造）

从 VLM/MLLM 出发加未来预测头。继承语言推理能力，更适合 long-horizon 任务。

- [UP-VLA](https://arxiv.org/abs/2501.18867)
- [CoT-VLA](https://arxiv.org/abs/2503.22020)
- [FLARE](https://arxiv.org/abs/2505.15659)
- [WorldVLA](https://arxiv.org/abs/2506.21539)
- [UniVLA](https://arxiv.org/abs/2506.19850)
- [DreamVLA](https://arxiv.org/abs/2507.04447)
- [FlowVLA](https://arxiv.org/abs/2508.18269)
- [F1](https://arxiv.org/abs/2509.06951)
- [RynnVLA-002](https://arxiv.org/abs/2511.17502)
- [MM-ACT](https://arxiv.org/abs/2512.00975)
- [VLA-JEPA](https://arxiv.org/abs/2602.10098)
- [LDA-1B](https://arxiv.org/abs/2602.12215)
- [VLAW](https://arxiv.org/abs/2602.12063)
- [WoG](https://arxiv.org/abs/2602.22010)
- [π0.7](https://arxiv.org/abs/2604.15483)

## 3.3 WAM from Scratch（从零训练）

世界模型和动作模型一起从零联合训。和经典 Dreamer / GameNGen 这条 RL 世界模型路线接得最直接。

- [DayDreamer](https://arxiv.org/abs/2206.14176)
- [DreamerV3](https://arxiv.org/abs/2301.04104)
- [Dynalang](https://arxiv.org/abs/2308.01399)
- [UniSim](https://arxiv.org/abs/2310.06114)
- [AVDC](https://arxiv.org/abs/2310.08576)
- [LAPO](https://arxiv.org/abs/2312.10812)
- [DIAMOND](https://arxiv.org/abs/2405.12399)
- [GameNGen](https://arxiv.org/abs/2408.14837)
- [GameGen-X](https://arxiv.org/abs/2411.00769)
- [NWM](https://arxiv.org/abs/2412.03572)
- [Moto](https://arxiv.org/abs/2412.04445)
- [Seer](https://arxiv.org/abs/2412.15109)
- [UVAM](https://arxiv.org/abs/2503.00200)
- [UWM](https://arxiv.org/abs/2504.02792)
- [CoMo](https://arxiv.org/abs/2505.17006)
- [LPS](https://arxiv.org/abs/2507.13340)
- [LeWorldModel](https://arxiv.org/abs/2603.19312)
- [WAV](https://arxiv.org/abs/2604.01985)
- [Being-H0.7](https://arxiv.org/abs/2601.12993)

---

# 4. World Model as Simulator（不当 policy，当训练/评估环境）

世界模型本身当 sim 用——给策略训 RL、给策略评估打分。**Sim-to-real 的另一种解法**：不再追求把 sim 做得像 real，而是让 sim 从 real data 里学出来。

## 4.1 WM 内部跑 RL · Learned Simulator

策略在学得的世界模型里跑 PPO/GRPO/SAC——把"无数次真机试错"换成"无数次脑内试错"。UniSim 开山，VLA-RFT / WMPO / World4RL 把它做成单卡级别的 VLA 后训练。

- [DayDreamer](https://arxiv.org/abs/2206.14176)
- [UniSim](https://arxiv.org/abs/2310.06114)
- [DreamerV3](https://arxiv.org/abs/2301.04104)
- [PlaNet](https://arxiv.org/abs/1811.04551)
- [Dream to Control](https://arxiv.org/abs/1912.01603)
- [DreamerV2](https://arxiv.org/abs/2010.02193)
- [Transformer-based WM (IRIS)](https://arxiv.org/abs/2209.00588)
- [MoDem-V2](https://arxiv.org/abs/2310.08576)
- [VIPER](https://arxiv.org/abs/2305.14343)
- [Diffusion Reward](https://arxiv.org/abs/2311.12116)
- [RWM-U](https://arxiv.org/abs/2504.16680)
- [DiWA](https://arxiv.org/abs/2508.03645)
- [World4RL](https://arxiv.org/abs/2509.19080)
- [Dreamer 4](https://arxiv.org/abs/2509.24527)
- [World-Env](https://arxiv.org/abs/2509.24948)
- [VLA-RFT](https://arxiv.org/abs/2510.00406)
- [PhysWorl](https://arxiv.org/abs/2511.07416)
- [WMPO](https://arxiv.org/abs/2511.09515)
- [SRPO](https://arxiv.org/abs/2511.15605)
- [ProphRL](https://arxiv.org/abs/2511.20633)
- [GenReward](https://arxiv.org/abs/2512.00961)
- [RoboScape-R](https://arxiv.org/abs/2512.03556)
- [World-Gymnast](https://arxiv.org/abs/2602.02454)
- [RWML](https://arxiv.org/abs/2602.05842)
- [RISE](https://arxiv.org/abs/2602.11075)
- [GigaBrain-0.5M](https://arxiv.org/abs/2602.12099)
- [RehearseVLA](https://arxiv.org/abs/2509.24948)

## 4.2 Co-Evolution（策略与 WM 互相打磨）

不再只用固定 WM 训策略——失败 rollout 反过来纠正 WM，更新过的 WM 再回训策略。2026 H1 兴起。

- [World-VLA-Loop](https://arxiv.org/abs/2602.06508)
- [VLAW](https://arxiv.org/abs/2602.12063)
- [WoVR](https://arxiv.org/abs/2602.13977)
- [PlayWorld](https://arxiv.org/abs/2603.09030)
- [VLA-MBPO](https://arxiv.org/abs/2603.20607)
- [ViVa](https://arxiv.org/abs/2604.08168)

## 4.3 WM for Imitation Learning（生成训练数据）

世界模型当数据工厂——给目标条件，直接 rollout 出训练 trajectory。

- [DREMA (Dream Manipulation)](https://arxiv.org/abs/2412.16832)
- [RoboScape](https://arxiv.org/abs/2509.03556)
- [Ctrl-World](https://arxiv.org/abs/2509.xxxxx)
- [DreamGen](https://arxiv.org/abs/2505.12705)
- [RoboDreamer](https://arxiv.org/abs/2404.12377)
- [ManipDreamer](https://arxiv.org/abs/2505.xxxxx)
- [PhysWorld](https://arxiv.org/abs/2511.07416)

## 4.4 WM for Evaluation / MPC

把 WM 当离线评估器：候选动作在 WM 里展开 rollout 打分。

- [TD-MPC2](https://arxiv.org/abs/2310.16828)
- [WorldEval](https://arxiv.org/abs/2505.19017)
- [WorldGym](https://arxiv.org/abs/2506.00613)
- [GPC](https://arxiv.org/abs/2502.00622)
- [IRASim](https://arxiv.org/abs/2406.14540)
- [Veo Evaluator (Gemini Robotics)](https://arxiv.org/abs/2512.10675)
- [Scalable Policy Evaluation](https://arxiv.org/abs/2511.11520)
- [DreamPlan](https://arxiv.org/abs/2603.16860)
- [LeWorldModel](https://arxiv.org/abs/2603.19312)
- [Interactive World Simulator](https://arxiv.org/abs/2603.08546)
- [dWorldEval](https://arxiv.org/abs/2604.22152)
- [WorldArena](https://arxiv.org/abs/2603.xxxxx)
- [FFDC-WAM](https://arxiv.org/abs/2605.06222)

---

# 5. Robotic Video World Models（Foundation-scale）

机器人专用视频生成模型——能力级别从"凭想象画一段"逐步演化到"foundation-scale 通用世界引擎"。

## 5.1 Video as Imagination
不要求动作可控、不要求物理一致，先把"长得对"做出来。

- [UniPi](https://arxiv.org/abs/2302.00111)
- [VLP](https://arxiv.org/abs/2310.10625)
- [Dreamitate](https://arxiv.org/abs/2406.16862)
- [RoboDreamer](https://arxiv.org/abs/2404.12377)
- [ManipDreamer](https://arxiv.org/abs/2505.xxxxx)
- [DreMa](https://arxiv.org/abs/2412.16832)
- [DreamGen](https://arxiv.org/abs/2505.12705)
- [EnerVerse](https://arxiv.org/abs/2501.01895)

## 5.2 Action-Controllable Video WM

接受动作序列作为条件输入，输出对应未来视频——可交互 simulator 的前提。

- [IRASim](https://arxiv.org/abs/2406.14540)
- [RoboEnvision](https://arxiv.org/abs/2506.22007)
- [RoboMaster](https://arxiv.org/abs/2506.xxxxx)
- [Ctrl-World](https://arxiv.org/abs/2509.xxxxx)
- [EnerVerse-AC](https://arxiv.org/abs/2505.xxxxx)
- [Interactive World Simulator](https://arxiv.org/abs/2603.08546)
- [EVA](https://arxiv.org/abs/2604.xxxxx)
- [Inverse Probabilistic Adaptation](https://arxiv.org/abs/2504.15369)

## 5.3 Structure-Aware Generation

加入物理 / 几何 / 交互先验，保证生成视频物理自洽。

- [Mask2IV](https://arxiv.org/abs/2509.xxxxx)
- [TesserAct](https://arxiv.org/abs/2504.20995)
- [RoboVIP](https://arxiv.org/abs/2603.xxxxx)
- [PhysWorld](https://arxiv.org/abs/2511.07416)
- [3DFlowAction](https://arxiv.org/abs/2506.06199)

## 5.4 Foundation-Scale Video World Models

大规模通用视频世界模型——参数 + 数据两端拉到 foundation 量级。

- [Genie](https://arxiv.org/abs/2402.15391)
- [Genie Envisioner](https://arxiv.org/abs/2508.05635)
- [Cosmos](https://arxiv.org/abs/2501.03575)
- [Cosmos Predict 2.5](https://arxiv.org/abs/2509.xxxxx)
- [Vid2World](https://arxiv.org/abs/2506.xxxxx)
- [DreamDojo](https://arxiv.org/abs/2602.06949)
- [WoW](https://arxiv.org/abs/2510.xxxxx)
- [UnifoLM-WMA-0 (Unitree)](https://arxiv.org/abs/2509.xxxxx)
- [GigaWorld-0](https://arxiv.org/abs/2510.19430)
- [ABot-PhysWorld](https://arxiv.org/abs/2511.xxxxx)
- [Yume](https://arxiv.org/abs/2507.17744)
- [Matrix-Game](https://arxiv.org/abs/2506.18701)
- [WorldMem](https://arxiv.org/abs/2504.12369)
- [PlayerOne](https://arxiv.org/abs/2506.09995)
- [The Matrix](https://arxiv.org/abs/2412.03568)
- [GameFactory](https://arxiv.org/abs/2501.08325)
- [Puffin](https://arxiv.org/abs/2510.086735)
- [CoLA-World](https://arxiv.org/abs/2510.26433)
- [NitroGen](https://arxiv.org/abs/2601.02427)
- [Learning Latent Action WM](https://arxiv.org/abs/2601.05230)
- [PointWorld](https://arxiv.org/abs/2601.03782)

---

# 6. Latent / Symbolic World Models

不预测像素的紧耦合 WM——latent neural representation 或 symbolic representation。

## 6.1 Neural Latent

未来在 embedding 空间预测，不渲染像素——继承 LeCun JEPA 路线，训练效率最高，可解释性最弱。V-JEPA 2/2.1 是 Meta 主力，VLA-JEPA / WoG / DIAL 把它接到机器人控制上。

- [FLARE](https://arxiv.org/abs/2505.15659)
- [V-JEPA 2](https://arxiv.org/abs/2506.09985)
- [V-JEPA 2.1](https://arxiv.org/abs/2603.14482)
- [VLA-JEPA](https://arxiv.org/abs/2602.10098)
- [JEPA-VLA](https://arxiv.org/abs/2602.11832)
- [VISTA](https://arxiv.org/abs/2602.10983)
- [WoG](https://arxiv.org/abs/2602.22010)
- [DIAL](https://arxiv.org/abs/2603.29844)
- [AIM](https://arxiv.org/abs/2604.11135)
- [DexWorldModel](https://arxiv.org/abs/2604.16484)
- [AdaWorld](https://arxiv.org/abs/2503.18938)

## 6.2 Symbolic / Planner-Facing WM

谓词、对象关系、affordance、因果过程——给经典 planner 用的世界模型抽象。和 neural latent 互补：可解释、可组合，但难以处理感知细节。

- [Liang et al. 2025c](https://arxiv.org/abs/2505.xxxxx)
- [Athalye et al. 2026](https://arxiv.org/abs/2602.xxxxx)
- [3D-VLA](https://arxiv.org/abs/2403.09631)

---

# 7. WAM 训练数据生态

S2 把数据按"来源"分四类——和 VLA 不同的是 WAM 更能消化无动作标注的数据（egocentric video、play data）。

## 7.1 Robot-Centric Teleoperation Datasets

对齐的 state-action 对，sim-to-real gap 最小，但采集贵且覆盖窄。Open X-Embodiment 是跨 22 机器人本体的总聚合，DROID 主打 in-the-wild 多样性。

- [QT-Opt](https://arxiv.org/abs/1806.10293)
- [MIME](https://arxiv.org/abs/1810.07121)
- [RoboNet](https://arxiv.org/abs/1910.11215)
- [RoboTurk](https://arxiv.org/abs/1911.04052)
- [Bridge](https://arxiv.org/abs/2109.13396)
- [MT-Opt](https://arxiv.org/abs/2104.08212)
- [BC-Z](https://arxiv.org/abs/2202.02005)
- [Language-Table](https://arxiv.org/abs/2210.06407)
- [RT-1 Dataset](https://arxiv.org/abs/2212.06817)
- [BridgeData V2](https://arxiv.org/abs/2308.12952)
- [Cable-Routing](https://arxiv.org/abs/2307.08927)
- [RH20T](https://arxiv.org/abs/2307.00595)
- [Open X-Embodiment](https://arxiv.org/abs/2310.08864)
- [DROID](https://arxiv.org/abs/2403.12945)

## 7.2 Portable Human Demonstration

便携式硬件采人类演示，再重定向到机器人——绕开真机采集瓶颈。UMI 用 GoPro 手持式 gripper 在野外采数据，比真机快 3 倍；DexCap 用 EMF 手套捕捉灵巧操作。

- [UMI](https://arxiv.org/abs/2402.10329)
- [DexCap](https://arxiv.org/abs/2403.07788)
- [ALOHA](https://arxiv.org/abs/2304.13705)
- [GELLO](https://arxiv.org/abs/2309.13037)

## 7.3 Simulation

有特权物理监督、可规模化变种。SynGrasp-1B 提供 billion 级合成抓取轨迹；MimicGen/GenSim/RoboGen 是自动生成 sim 任务和轨迹的引擎。

- [RoboCasa](https://arxiv.org/abs/2406.02523)
- [RoboGen](https://arxiv.org/abs/2311.01455)
- [MimicGen](https://arxiv.org/abs/2310.17596)
- [GenSim](https://arxiv.org/abs/2310.01361)
- [RoboTwin 2.0](https://arxiv.org/abs/2506.18088)
- [SynGrasp-1B](https://arxiv.org/abs/2505.03233)

## 7.4 Internet-Scale Egocentric Video

人类第一视角视频——WAM 训练的关键长尾，没有动作标签但有海量"世界如何演化"的先验。WAM 比纯 VLA 更能消化这类无标注数据。

- [Ego4D](https://arxiv.org/abs/2110.07058)
- [EpicKitchens](https://arxiv.org/abs/2006.13256)
- [HOI4D](https://arxiv.org/abs/2203.01577)

---

# 8. 经典 World Model（奠基工作，不限机器人）

读 WAM 必须知道的经典 World Model 论文——RL/控制圈的奠基工作。

## 8.1 Dreamer 系列

Hafner 团队从 2018 PlaNet 一路演化到 2025 DreamerV3 + 2026 Dreamer4——经典 latent world model + actor-critic 范式，至今仍是 model-based RL 的事实标杆。DayDreamer 是首次在真机上跑 Dreamer 的工作。

- [PlaNet](https://arxiv.org/abs/1811.04551)
- [Dream to Control (Dreamer)](https://arxiv.org/abs/1912.01603)
- [DreamerV2](https://arxiv.org/abs/2010.02193)
- [DayDreamer](https://arxiv.org/abs/2206.14176)
- [DreamerV3](https://arxiv.org/abs/2301.04104)
- [Dreamer 4](https://arxiv.org/abs/2509.24527)

## 8.2 Transformer-based World Models

放弃 RSSM/RNN backbone，换成 transformer 做世界建模——IRIS / TWM 是 Atari 上首批成功的尝试，Genie/DIAMOND/GameNGen 把它扩展到 playable game 级别。

- [IRIS (Transformer-based WM)](https://arxiv.org/abs/2209.00588)
- [TWM (Transformer WM 100k)](https://arxiv.org/abs/2303.07109)
- [Genie](https://arxiv.org/abs/2402.15391)
- [DIAMOND](https://arxiv.org/abs/2405.12399)
- [GameNGen](https://arxiv.org/abs/2408.14837)

## 8.3 JEPA / Latent

LeCun 力推的 Joint Embedding Predictive Architecture——核心主张是"在 latent 空间预测而非像素空间"。I-JEPA 做图像，V-JEPA 2 做视频，后者已经接到 WAM 上（VLA-JEPA、JEPA-VLA）。

- [A Path Towards AMI (LeCun)](https://openreview.net/forum?id=BZ5a1r-kVsf)
- [I-JEPA](https://arxiv.org/abs/2301.08243)
- [V-JEPA 2](https://arxiv.org/abs/2506.09985)

## 8.4 历史奠基（pre-2020）

WAM 早期源头——Oh et al. 2015 ACVP 是首篇明确做 action-conditional video prediction 的工作，可看作整个 WAM 路线的起点。

- [ACVP (Action-Conditional Video Prediction)](https://arxiv.org/abs/1507.08750)
- [CLASP](https://arxiv.org/abs/1806.09655)
- [CADDY](https://arxiv.org/abs/2101.12195)
- [Playable Environments](https://arxiv.org/abs/2203.01914)

---

# 9. Navigation / Driving WM（应用线）

WM 不止用在机器人 manipulation——navigation 和 autonomous driving 是另两条独立线。

## 9.1 Navigation WM

世界模型用于导航——预测"如果我往那个方向走，场景会变成啥样"，再用预测画面选最优动作。NavigateDiff / VISTA / ForesightNav 是这条线代表，相关综述见 navigation 专题。

- [Dynalang](https://arxiv.org/abs/2308.01399)
- [NavDreamer / WMNav](https://arxiv.org/abs/2503.02247)
- [NavigateDiff](https://arxiv.org/abs/2502.13894)
- [VISTA (Generative Visual Imagination)](https://arxiv.org/abs/2505.07868)
- [ForesightNav](https://arxiv.org/abs/2504.16062)
- [Do Visual Imaginations Improve VLN?](https://arxiv.org/abs/2503.16394)

## 9.2 Autonomous Driving WM

自动驾驶世界模型——预测周边车辆/行人未来轨迹，给 planner 做 lookahead。OccLLaMA 做 occupancy-language-action，DriveDreamer / GenAD / WoVoGen 主打 scene generation。

- [OccLLaMA](https://arxiv.org/abs/2409.03272)
- [DriveVLM](https://arxiv.org/abs/2402.12289)
- [EMMA](https://arxiv.org/abs/2410.23262)
- [DriveDreamer](https://arxiv.org/abs/2309.09777)
- [GenAD](https://arxiv.org/abs/2403.09630)
- [WoVoGen](https://arxiv.org/abs/2312.02934)

---

# 10. 选读建议（按身份）

| 你是 | 应该先读 |
|---|---|
| **想入门 WAM 概念** | S2 综述 `2605.12090` + S1 综述 `2605.00080`（Section 1-3） |
| **做 cascaded WAM 工程** | UniPi → π0.7 → NovaFlow → Vidar |
| **做 joint diffusion WAM** | UWM → Cosmos Policy → DreamZero → Fast-WAM |
| **做 latent WM (JEPA 流)** | V-JEPA 2 → VLA-JEPA → WoG → DIAL |
| **做 WM-in-the-loop RL** | UniSim → World4RL → VLA-RFT → WMPO |
| **做 foundation video WM** | Genie → Genie Envisioner → Cosmos → GigaWorld-0 |
| **关心 WAM 数据训练** | Open X-Embodiment → AgiBot World → EgoVLA → DreamGen |
| **关心评估** | WorldEval → WorldGym → dWorldEval → Gemini × Veo |
