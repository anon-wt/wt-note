|| a|b||
||产品||标签||含义||逻辑||对接人||所属业务域||开发者||
|卡豆|累计放款金额|区分段内，端外，和全部， {color:#FF0000}做成三个标签{color}|SELECT
 (CASE
 t2.whether_in_app 
 WHEN '0' THEN '端外' 
 WHEN '1' THEN'端内' else '无' end) as whetherInApp,
 sum( t2.amount ) 
 from t_order t1 LEFT JOIN t_order_credit t2 on t1.order_id = t2.order_id
 where t1.register_id = 1691760608086994946
 and t2.product_code = 'ddq'
 AND t2.order_status IN ( 'loaned', 'normalRepayment', 'clearUp' ) 
GROUP BY|彭焱东|贷前| |
|导流平台|N天内打开【借钱tab页】次数|已有，增加90 180|卡卡：
借钱tab点击事件：
loantabpagewiew_product_list_result
豆豆：
借钱tab点击：
kkplatform_show| 刘学良，刘秋杰| 贷前| |
| |N天内打开APP次数|已有，增加90 180|卡卡：OpenApp
豆豆：OpenApp| 刘学良，刘秋杰|贷前| |
| |最近一次打开APP距今天数|已有| | | | |
| |最近一次打开【借钱tab页】距今天数|已有| | | | |
| |N天内导流平台授信成功产品数| 3,7,15,30,60，90
做成6个标签|select count(DISTINCT sku_key) from t_business_order where register_id = #\{registerId} and status = 'CREDIT_FINISHED'
 and created_time between #\{startTime} and #\{endTime};
  | |
| |N天内导流平台交单产品数| 3,7,15,30,60，90做成6个标签|
|select count(DISTINCT sku_key) from t_business_order where register_id = #\{registerId} and status = 'CREDIT_APPROVING'
 and created_time between #\{startTime} and #\{endTime};|
 | | | |
| |N天内导流平台提现产品数| 3,7,15,30,60，90
做成6个标签| 
|select count(DISTINCT sku_key) from t_business_order where register_id = #\{registerId} and status = 'WITHDRAW_LOAN_WAITING'
 and created_time between #\{startTime} and #\{endTime};|
| | | |
| |放款利率| |API:
select sku_key,yearly_rate from t_platform_order_flow where register_id = 1234567789 and `status` = 'SUCCESS' order by created_time desc
H5:
select sku_key,yearly_rate from t_platform_tripartite_order where register_id = 1234567789 and withdraw_status = 'SUCCESS' order by created_time desc| | | |
| |导流产品首复贷区分| |select sku_key,loan_type,created_time from t_business_order where register_id = 1693586927258832897 order by created_time desc;| | | |
| |N天内单产品点击次数| 已有，新增判断条件|老项目
卡卡：
tab页产品点击：loantabpagewiew_product_list_click
授信等待页推荐产品点击：waitingpageview_product_click
豆豆：A20002（tab页和授信等待页未做区分）
新项目（8.24上线）
jieqian02（卡豆都是这个埋点，通过spuKey是ddq或者ccl区分）| | | |
| |首贷出额未提现滞留天数| | | | | |
| |复贷出额未提现滞留天数| | | | | |
| |复贷已结清未授信滞留天数| | | | | |

 
