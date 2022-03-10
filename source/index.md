| 版本号 | 修订人 | 更新日志        | 日期       |
| ------ | ------ | --------------- | ---------- |
| 1.0.0  | 王梦思 | 提供开放接口    | 2019-10-31 |
| 1.0.1  | 王梦思 | 增加一些hrv指标 | 2019-12-18 |


```
注意: 该接口为服务器端调用，非客户端调用

使用步骤:

1. 向我们算法服务器接口提供者索要appSecret和appKey

2. 提供调用者服务器IP地址（白名单机制）,否则无法调用

3. 调用算法接口
```


### 服务器地址

```
正式服: https://ecg.protontek.com/ecg-algorithm

测试服: https://ecgtest.protontek.com/ecg-algorithm（测试请使用）
```

| 接口名称 | 接口地址                | 请求方法 | 备注       |
| -------- | ----------------------- | -------- | ---------- |
| 算法调用 | /openapi/algorithm/call | POST     | body体传参 |

| 请求头       | 字段用途         | 字段格式         | 备注           |
| ------------ | ---------------- | ---------------- | -------------- |
| appKey       | appKey           | String           | 算法服务器提供 |
| appSecret    | appSecret        | String           | 算法服务器提供 |
| content-type | POST请求数据格式 | application/json |                |

| 参数         | 字段用途     | 字段格式 | 备注                                   |
| ------------ | ------------ | -------- | -------------------------------------- |
| callId       | 调用者的id   | String   | 必须唯一，比如可以为报告id             |
| dataSource   | 数据来源     | String   | 可以为调用者公司名称或者项目名         |
| rawData      | 原始心电数据 | String   | float值，用英文逗号隔开                |
| callBackPath | 回调地址     | String   | 回调服务器必须支持POST请求，body体传参 |

### 回调数据参数

| 参数名               | 字段用途               | 字段格式 | 备注                                                         |
| -------------------- | ---------------------- | -------- | ------------------------------------------------------------ |
| callId               | 调用算法传递的唯一id   | String   |                                                              |
| AF                   | 房颤                   | 0/1      | 0无 1有                                                      |
| PB                   | 早搏                   | 0/1      | 0无 1有                                                      |
| aveHR                | 平均心率               | Integer  |                                                              |
| maxHR                | 最大心率               | Integer  |                                                              |
| minHR                | 最小心率               | Integer  |                                                              |
| peakSum              | 心博总数               | Integer  |                                                              |
| heartPace            | 心率快慢               | Integer  | 0正常、1心动过缓、2心动过速                                  |
| modelResult          | 模型结果               | Integer  |                                                              |
| heartSlowTime        | 心动过缓时间           | Integer  | 毫秒                                                         |
| heartFastTime        | 心动过速时间           | Integer  | 毫秒                                                         |
| hrvScore             | HRV分数                | Integer  |                                                              |
| hrvIndex             | HRV级别                | Integer  |                                                              |
| alcoholRiskScore     | 饮酒风险分数           | Integer  |                                                              |
| alcoholRiskIndex     | 饮酒风险级别           | Integer  |                                                              |
| alcoholRiskDecrease  | 饮酒风险减分项         | Integer  |                                                              |
| mentalStressScore    | 精神压力分数           | Integer  |                                                              |
| mentalStressIndex    | 精神压力级别           | Integer  |                                                              |
| mentalStressDecrease | 精神压力减分项         | Integer  |                                                              |
| sdnn                 | RR间期标准差           | Float    |                                                              |
| rmssd                | 相邻RR间期差值到标准差 | Float    |                                                              |
| tp                   | 总功率                 | Float    |                                                              |
| fatigueScore         | 疲劳度指标             | Float    |                                                              |
| vlf                  | 超低频功率             | Float    |                                                              |
| lf                   | 低频功率               | Float    |                                                              |
| hf                   | 高频功率               | Float    |                                                              |
| LFnorm               | 归一化低频功率         | Float    |                                                              |
| HFnorm               | 归一化高频功率         | Float    |                                                              |
| LFHFRatio            | 低频和高频功率比值     | Float    |                                                              |
| filePath             | 文件路径               | String   | 该文件存储在算法服务器，文件<br>为json格式，数据包含原始数据<br>，滤波数据，建议及时下载存储<br>到调用者服务器 |


```
注意事项：
接口调用限制了ip，需要将调用服务器ip加入白名单，否则会禁止调用
