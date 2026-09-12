# 券商交易反欺诈检测（方法复现版）

对 13.8 万笔券商交易流水做端到端欺诈检测建模：行为特征工程 → 不平衡学习（折内 SMOTE / 类别权重）→ 模型对比与阈值策略 → 成本敏感决策。**测试集 AP 0.936、固定精确率 0.80 下欺诈召回率 90.5%**，较规则基线提升 36 个百分点。

**▶ 在线演示（浏览器直接打开）**：https://shutong-ge.github.io/fraud-detection-brokerage/

## 亮点
- 行为级特征：频次突增、金额偏离、设备信任等 velocity 特征是把召回推过 90% 的关键
- 严格防泄漏：SMOTE 仅在训练折内、阈值由 OOF 分数导出、另设 OOT 时间外验证（AP 0.916）
- 成本敏感双阈值分层：自动拦截 + 人工审核，总预期损失下降 89.6%
- 在线演示：风险决策台（阈值滑杆实时联动精确率/召回率/成本，数字全部来自真实模型产物）

## 文件
| 文件 | 说明 |
|---|---|
| 反欺诈检测_端到端建模.ipynb | 完整建模 notebook（已执行，含程序化自查） |
| index.html | 反欺诈运营工作台（5 视图，含 AI 调查员；模型在浏览器端真实推理） |

**在线演示**：https://shutong-ge.github.io/fraud-detection-brokerage/

## 数据与真实性声明
原实习数据涉密不可公开。本仓库为**方法复现版**：数据由行为级生成器合成（seed=42），交易日历为上交所真实日历、股票代码与价位量级真实锚定，欺诈模式按公开风控文献的接管场景（快速转出/洗仓/试探/拉抬/伪装）行为化生成，生成逻辑与校验在 notebook 内完整披露。

数据集（138,000 笔 × 30 列）体积较大未随仓库分发，生成逻辑与校验在 notebook 内完整披露，可邮件索取。

## 运行
notebook 依赖：pandas / scikit-learn / imbalanced-learn / matplotlib。逐 cell 运行即可复现全部数字。

---
### English Summary
End-to-end fraud detection on 138k brokerage transactions: behavioral feature engineering, imbalanced learning (in-fold SMOTE vs. class weights), model comparison and cost-sensitive thresholding. Test AP 0.936, **90.5% fraud recall at fixed precision 0.80** (+36pt over rule baseline), with leakage-safe validation (OOF thresholds, out-of-time check). Method-reproduction release on synthetic behavior-level data (real internship data is confidential); generation logic fully disclosed in the notebook.
