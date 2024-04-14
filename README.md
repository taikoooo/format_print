## format_print
> 一个用于格式化输出的库，主要功能包括多行输出刷新、全半角字符混合对齐、秒数及字节大小格式化等。

#### pip
``` shell
pip install format_print
```

#### 主要功能简介
- Unicode_len: 获取全半角混合字符串的长度
  > 半角字符长度为1，全角字符长度为2，以此计算总长度。
- Rehuman: 数字格式化
  > 将整数或浮点数转化为携带单位的字符串，目前包括：时长、字节，允许指定进制、单位、格式等。
- Respacing: 全半角混合字符串对齐
  > 为同时包含全角和半角的字符串设置对齐，全角字符长度视为半角字符的2倍。
- Rows_print: 多行输出
  > 主要用于多行字符串的刷新，可以指定输出起始行次、对齐方式

#### 简易示例
``` python
from format_print import Unicode_len, Rehuman, Respacing, Rows_print
import time

# Unicode_len
length = Unicode_len('该文本的长度：16').get_len()
print(length) # 16

# Rehuman
print(Rehuman(100000).from_size()) # 97.66KB
print(Rehuman(500).from_seconds()) # 00h08m20s
print('\n')

# Rows_print
Rows_print(
    '第1行\n这里是第2行',
    '^',
).print_str()
'''
   第1行
这里是第2行
'''

# Respacing
for i in range(37):
    print(
        Respacing(
            "[",
            ("=" * min(i, 12), 12, "<"),
            "进度：{:>3.2f}%".format(i / 36 * 100),
            ("=" * (i - 24), 12, "<"),
            "]",
            space = '_'
        ).get_str(),
        end = '\r'
    )
    time.sleep(0.3)
print()
'''
生成进度条
[============进度：50.00%____________]
'''
```