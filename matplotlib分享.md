# Matplotlib使用分享
## 01-Introduction
```python
from matplotlib import pyplot as plt

# plt.xkcd()
# plt.style.use('classic')
# print(plt.style.available)

ages_x = [25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35]

py_dev_y = [45372, 48876, 53850, 57287, 63016,
            65998, 70003, 70000, 71496, 75370, 83640]
plt.plot(ages_x, py_dev_y, label='Python')

js_dev_y = [37810, 43515, 46823, 49293, 53437,
            56373, 62375, 66674, 68745, 68746, 74583]
plt.plot(ages_x, js_dev_y, label='JavaScript')

dev_y = [38496, 42000, 46752, 49320, 53200,
         56000, 62316, 64928, 67317, 68748, 73752]
plt.plot(ages_x, dev_y, color='#444444', linestyle='--', label='All Devs')

plt.xlabel('Ages')
plt.ylabel('Median Salary (RMB)')
plt.title('Median Salary (RMB) by Age')

plt.legend()
plt.grid()
plt.tight_layout()

#plt.savefig('plot.png')

plt.show()
```

## 02-BarCharts
### 2.1基础柱状图
```python
import numpy as np
from matplotlib import pyplot as plt

ages_x = [25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35]

py_dev_y = [45372, 48876, 53850, 57287, 63016,
            65998, 70003, 70000, 71496, 75370, 83640]

js_dev_y = [37810, 43515, 46823, 49293, 53437,
            56373, 62375, 66674, 68745, 68746, 74583]

dev_y = [38496, 42000, 46752, 49320, 53200,
         56000, 62316, 64928, 67317, 68748, 73752]

x_indexes = np.arange(len(ages_x))  # 对x轴坐标进行处理
width = 0.25  # matplotlib柱子默认宽度为0.8，多条柱子要注意宽度设置

plt.bar(x_indexes - width, py_dev_y, width=width,
        color="#008fd5", label='Python')
plt.bar(x_indexes, js_dev_y, width=width, color="#e5ae38", label='JavaScript')
plt.bar(x_indexes + width, dev_y, width=width,
        color="#444444", label="All Devs")

plt.xlabel('Ages')  # x轴标题
plt.ylabel('Median Salary (RMB)')  # y轴标题
plt.title('Median Salary (RMB) by Age')  # 标题
plt.xticks(x_indexes, ages_x)  # 设置x轴标签

plt.legend()
plt.tight_layout()

plt.show()
```

### 2.2使用传统方式读取CSV文件并使用柱状图分析
```python
import csv
from collections import Counter
from matplotlib import pyplot as plt

with open('data.csv') as csv_file:
    csv_reader = csv.DictReader(csv_file)

    language_counter = Counter()

    for row in csv_reader:
        language_counter.update(row['LanguagesWorkedWith'].split(';'))
    
languages = []
popularity = []

for item in language_counter.most_common(15):
    languages.append(item[0])
    popularity.append(item[1])

plt.bar(languages, popularity)

plt.xlabel('Programming Languages')  # x轴标题
plt.ylabel('The Number Of People Who Use')  # y轴标题
plt.title('The Most Popular Languages')  # 标题

plt.tight_layout()

plt.show()
```

### 2.3使用pandas读取CSV文件并使用柱状图分析
```python
import pandas as pd
from matplotlib import pyplot as plt

data = pd.read_csv('data.csv')
ids = data['Responder_id']
lang_responses = data['LanguagesWorkedWith']

language_counter = Counter()

for response in lang_responses:
    language_counter.update(response.split(';'))
    
languages = []
popularity = []

for item in language_counter.most_common(15):
    languages.append(item[0])
    popularity.append(item[1])

languages.reverse()  # 倒序
popularity.reverse()  # 倒序

plt.barh(languages, popularity)

plt.xlabel('The Number Of People Who Use')  # x轴标题
plt.title('The Most Popular Languages')  # 标题

plt.tight_layout()

plt.show()
```
