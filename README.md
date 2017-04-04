![](http://p3.pstatp.com/large/17f500006dcb4be47983)

`cage`: 北京二手房购房资金计算.

Last update: 2017.04.04

# 适用

北京城区二手商品房, 公房, 二类经济适用房.

# 功能

- 针对买家的计算. 将买家的资金能力转换为其购买各类型房屋可承受的上限.
- 针对某套房子的计算
  - 考虑买家能力, 优化计算不同购房方案, 如:
    - 最小准备金方案
    - 最小月供方案
  - 不考虑资金约束情况下, 计算购房方案

# 使用

```python
from pycage import Buyer, House
```

针对某买家计算:

```python
buyer = Buyer()

# 设定买家参数 
buyer.is_first = False # 是否首套
buyer.age = 36 # 买家年龄
buyer.max_prepared_money = 800.0 # 初始总资金
buyer.num_month_reserved = 36 # 预留多少个月的月供
buyer.other_money_reserved = 20.0 # 其它预留资金
buyer.max_monthly_repayment = 3.0 # 可承受月供上限
buyer.loan_from_fund_is_wanted = True # 是否需要公积金贷款

# 计算买家购房能力
buyer.cal_limits()
```

针对某套房子计算:

```python
# 用buyer初始化house
house = House(buyer)

# 设定房屋参数
house.type = "public" # 类型. "public": 公房; "commercial": 商品房; "affordable2": 二类经适房
house.price = 1000.0 # 实际成交价
house.original_price = 200.0 # 房屋原值 (如果原值不可溯, 设为0)
house.num_holding_years = 5 # 房产证或契税票下发年数
house.is_only = False # 是否业主 (家庭为单位) 在京唯一住房
house.area = 120.0 # 房屋面积
house.building_year = 2000 # 建筑年代
house.building_structure = "steel" # 建筑结构: "steel": 钢混; "brick": 砖混
house.position = 5 # 位置: 5: 5环内; 6: 5-6环; 7: 6环外
house.monthly_rent = 0.9 # 估计月租金 (如自住设为0)

# 购房方案计算
house.cal_plans()
```

# License

MIT