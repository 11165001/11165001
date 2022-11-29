### Hi there 👋

<!--
**11165001/11165001** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->


!pip install yfinance
import yfinance as yf

msft = yf.Ticker("AAPL")

# get stock info
msft.info

# get historical market data
hist = msft.history(period="1y")
#hist[["Close", "Volume"]]

v0 = hist['Volume'].mean()
v0
data = hist [['Close', 'Volume']]
data
data.shape
print(data.iloc[0, 1])
print(data.iloc[-1])
print(data.iloc[data.shape[0]-1, 1])

s_sum = 0
for i in range(0, data.shape[0]-1):
  s_sum = s_sum + data.iloc[i, 1]
print(s_sum)
#for j in range(0, data.shape[0]):
  #print(int(data.iloc[j, 0]), int(data.iloc[j, 1]))
#if(s_sum < v0):
print(data.iloc[251, 0] - data.iloc[0, 0])

amt = list(hist[["Volume"]].iloc[:, 0])
Screen Shot 2022-11-9 at 下午 06.51.png

from pandas.core.indexes.extension import deprecate_ndim_indexing
import pandas as pd
import numpy as np

#設定一個空的k及dp, 初值皆為NaN
k = np.empty(len(hist))
dp = np.empty(len(hist))

k[:] = np.nan
dp[:] = np.nan

#將Volumn存在volume中
volume = list(hist[["Volume"]].iloc[:, 0])

#================================
#任意設定一個V0值
#================================
V0 = 1000000000

#找出每個索引值的k
for i in range(0, len(hist)):
    t=np.nan
    for j in range(i+1):
        if sum(volume[j:i]) < V0:
            t=j 
            break
    k[i]=t 

#找出每個索引值的dp
for i in range(0, len(hist)):
    t=[]
    for j in range(int(k[i]), i):
        t.append(volume[i]-volume[j])
  
    if len(t)==0:
        dp[i] = np.nan
    else:
        dp[i] = max(t)

#印dp
dp
V0 = 10000
s_diff = [251, 0]
s_date = ["Date"]
n=251
for j in range(1, 251+1):
    v_sum = n        #Vk+Vk+1+......+Vn
    if(v_sum<V0):
      s_diff.append(251 - s_sum)
      s_date.append([n,j])
    
    dpn = max(s_diff) 
    ddn = [Daten,Datej]

Screen Shot 2022-11-9 at 下午 06.53.png

#將dp(list)轉成df_dp(DataFrame)
df_dp = pd.DataFrame(dp)

#平均數/標準誤
m = float(df_dp.mean())
se = float(df_dp.std() / len(hist)**0.5)

#推論x值(假設a=0.05)
print(m-1.96*se)
