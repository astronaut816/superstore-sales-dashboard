# 🛒 Superstore Sales Performance Analysis Dashboard

## 📖 项目背景 (Project Background)
零售行业不仅关注销售额的增长，更关注利润的质量。本项目基于 Superstore 2014-2017 年的订单数据集，从**销售趋势、区域市场、品类结构、客户细分、折扣风险**以及**配送效率**等多个维度进行全面诊断。旨在通过数据驱动的方式，识别高增长业务线，定位亏损风险点，并为管理层提供可落地的经营策略。

## 📁 数据集说明 (Dataset Overview)
数据来源于 `Superstore_Orders_Data.csv`，为订单行级数据，包含约 9000+ 条记录与 21 个字段：
- **时间维度**：`Order_Date` , `Ship_Date` 
- **地理维度**：`Region` , `State` , `City` 
- **产品维度**：`Category` , `Sub_Category` , `Product_Name` 
- **财务指标**：`Sales` , `Profit` , `Discount` , `Quantity` 
- **客户与物流**：`Segment` , `Ship_Mode` 

## 📊 看板预览 (Dashboard Preview)
![Superstore Dashboard](dashboard-overview.png)

### 💡 核心业务洞察 (Key Insights)
通过 Power BI 看板与 SQL 交叉分析，得出以下核心发现：
1. **整体经营稳健，但利润率偏低**：2014-2017 累计销售额约 2.3M，总利润 286.4K，整体毛利率仅为 **12.47%**。同比增长达 46.88%，业务规模仍在扩张。
2. **折扣与利润强负相关**：通过"折扣-利润散点图"发现，当折扣率超过 **20%** 时，订单利润显著下滑，甚至出现大规模亏损红色散点集中，高折扣促销策略需要严格限制。
3. **区域与品类结构不均**：Standard Class 配送占比高达 59.12%；Consumer 客户群贡献了 50.56% 的销售额，是核心基本盘。部分子品类虽销售额高，但受高折扣拖累，常年处于亏损边缘。

## 🛠️ SQL 深度分析模块 (SQL Analysis Modules)
项目中的 `Superstore_Sales_Analysis.sql` 包含了从数据清洗到高级分析的完整链路：
- **数据质量检查**：检查空值、重复订单，确保数据口径准确。
- **多维度聚合汇总**：使用 `GROUP BY` 对区域、品类、配送模式、客户细分进行销售与利润拆分。
- **时间序列分析**：提取 Year/Month，并利用 `LAG()` 窗口函数计算月度销售**环比增长率**。
- **产品盈亏诊断**：使用 `HAVING SUM(Profit) < 0` 精准筛选出所有"长年亏损"的黑名单产品。
- **区域榜单排名**：结合 CTE 与 `RANK() OVER(PARTITION BY ...)` 计算各区域内销售额及利润 Top 1 的产品。
- **折扣利润测算**：按折扣率分组，计算不同折扣区间下的平均利润，为定价策略提供依据。

## 🗂️ 项目文件结构 (File Structure)
```text
superstore-sales-dashboard/
├── README.md                                     # 项目介绍文档
├── Superstore_Orders_Data.CSV                    # 原始订单数据集
├── Superstore_Sales_Analysis.sql                 # 完整SQL分析代码
├── Superstore_Sales_Data_Analysis_xkx.pbix       # Power BI 本地看板文件
└── dashboard-overview.png                        # 看板静态截图预览
