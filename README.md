# 仅用于学习日记，不可用于任何商业用途
#对基于用户和物品的协同推荐加入时间衰退因子
#1、整理数据  {userid，{itemid:record,timestamp}},  对record和timestamp命名  方便后面调用
#2、将数据分为train和test
#3、生成协同文件  
#基于用户的协同推荐公式为 （sum（1/(1+alpha*abs(t_ui-t_vi)/（24*60*60）*1/math.log(1+len(users)））——i）/sqrt(u_i*v_i )
#alpha为时间衰退因子
#abs(t_ui-t_vi) 用户u对物品i评价的时间和用户v对物品i评价的时间的绝对值
#math.log(1+len(users)） users为对物品i的评价人数 惩罚人们商品
#u_i 用户u一共评价的商品
#v_i 用户v一共评价的商品
#生成的数据为{userid_u,{userid_v,相关分数}}
#4、推荐
#找到该用户最相关的前k个用户
#将这K个用户的相关分数分别去乘以这个K个用户对物品的评分
#剔除该用户已经评过分的进行前n个推荐
#5、评价
#在test中随机选m个用户
#分别找出给他们推荐的那个物品
#sum（将推荐物品和他们实际评价物品取交集的个数）/sum（推荐的物品数）
