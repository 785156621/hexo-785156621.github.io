---
title: mysql排行榜代码
tags:
  - MySQL
url: 228.html
id: 228
categories:
  - MySQL
  - SQL
date: 2017-09-26 16:27:00
---

显示前10位名次，并显示自己名次。 1.xxx 2.xxx ..... 10.xxxx 我的当前名次: 第xx名。 这样应该如何编写，主要就是如何显示自己名次。    

前十[SQL](https://www.baidu.com/s?wd=SQL&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Y3rjuWuHbkujI-Pjn4Pvcs0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EPjc1PWmYPHfL)：
[SELECT](https://www.baidu.com/s?wd=SELECT&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Y3rjuWuHbkujI-Pjn4Pvcs0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EPjc1PWmYPHfL) \* [FROM](https://www.baidu.com/s?wd=FROM&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Y3rjuWuHbkujI-Pjn4Pvcs0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EPjc1PWmYPHfL) \`some_table\`
    ORDER BY \`score\`
    [LIMIT](https://www.baidu.com/s?wd=LIMIT&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Y3rjuWuHbkujI-Pjn4Pvcs0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EPjc1PWmYPHfL) 10
自己名次如[ls](https://www.baidu.com/s?wd=ls&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Y3rjuWuHbkujI-Pjn4Pvcs0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EPjc1PWmYPHfL)：
[SELECT](https://www.baidu.com/s?wd=SELECT&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Y3rjuWuHbkujI-Pjn4Pvcs0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EPjc1PWmYPHfL) COUNT(\`score\`) [FROM](https://www.baidu.com/s?wd=FROM&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Y3rjuWuHbkujI-Pjn4Pvcs0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EPjc1PWmYPHfL) \`some_table\`
    [WHERE](https://www.baidu.com/s?wd=WHERE&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Y3rjuWuHbkujI-Pjn4Pvcs0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EPjc1PWmYPHfL)` score`>([SELECT](https://www.baidu.com/s?wd=SELECT&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Y3rjuWuHbkujI-Pjn4Pvcs0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EPjc1PWmYPHfL) \`score\`  [FROM](https://www.baidu.com/s?wd=FROM&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Y3rjuWuHbkujI-Pjn4Pvcs0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EPjc1PWmYPHfL) \`some_table\` [WHERE](https://www.baidu.com/s?wd=WHERE&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Y3rjuWuHbkujI-Pjn4Pvcs0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3EPjc1PWmYPHfL) id=#用户的id); 
就是获得比自己分数高的人有多少