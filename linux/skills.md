# linux使用技巧

1. 如果你知道怎么用sort/uniq来做集合交集、并集、差集能很大地促进你的工作效率。假设有两个文本文件a和b已解被 uniq了，那么，用sort/uniq会是最快的方式，无论这两个文件有多大（sort不会被内存所限，你甚至可以使用-T选项，如果你的/tmp目录很小）
```
1) cat a b | sort | uniq > c   # c is a union b 并集
2) cat a b | sort | uniq -d > c   # c is a intersect b 交集
3) cat a b b | sort | uniq -u > c   # c is set difference a - b 差集
```
2. vi字符串替换
```
1) :%s/vivian/sky/g(等同于 :g/vivian/s//sky/g) 替换每一行中所有 vivian 为 sky
2) :%s/vivian/sky/(等同于 :g/vivian/s//sky/) 替换每一行的第一个 vivian 为 sky
3) :g/vivian/s//sky/g  替换每一行中所有 vivian 为 sky
4) :s/vivian/sky/      替换当前行第一个 vivian 为 sky
5) :s/vivian/sky/g     替换当前行所有 vivian 为 sky
6) :n,$s/vivian/sky/ 替换第 n 行开始到最后一行中每一行的第一个 vivian 为 sky
7) :n,$s/vivian/sky/g 替换第 n 行开始到最后一行中每一行所有 vivian 为 sky
n 为数字，若 n 为 .，表示从当前行开始到最后一行
```