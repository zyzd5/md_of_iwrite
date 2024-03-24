### 人物属性
* EFT/Aki_Data/Server/database/globals.json
>SkillBoostPercent 技能提升百分比（数值越大升级越快）
SkillProgressRate 技能进度（数值越大升级越快）
SkillFatiguePerPoint 技能疲劳（相当于技能点获取，0为无上限）
### 战局时长
* Aki_Data\Server\database\locations\地图名\base.json
“EscapeTimeLimit” 分钟
bigmap 海关
woods 森林
lighthouse 灯塔
shoreline 海岸线
interchange 立交桥
rezervbase 储备站
factory4_night 工厂晚上
factory4_day 白天
laboratory 实验室
takovstreets 街区
### 空投
* Aki_Data\Server\configs\airdrop.json
airdropChancePercent”:空投几率 百分比
### 保险
* Aki_data/server/database/trader/54cb50c76803fa8b248b4571/base.json    # 俄商
```json
# 修改为
"max_return_hour":1,
"max_storage_time":96,
"min_payment":0,
"min_return_hour":0,
```
* Aki_data/server/configs/insurance.json
```json
"returnChancePercent": {
    "54cb50c76803fa8b248b4571": 100,
    "54cb57776803fa99248b456e": 100    
    }
```
```json
"returnTimeOverrideSeconds": 1,
"runIntervalSeconds": 10
```
### 仓库扩容
* X/Aki_Data/Server/database/templates/items
查找  
566abbc34bdc2d92178b4576 （标准版仓库代码）

566abbc34bdc2d92178b4576 （留守版仓库代码）

5811ce662459770f6f490f32  （准备逃离版仓库代码）

5811ce772459770e9e5f9532 （黑暗边缘版仓库代码）

修改 cellsV, 这个数值将决定你的仓库垂直行的数量
