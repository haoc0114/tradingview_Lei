# Tradingview 雷公雙均線&乖離
1. 隨便搜尋一個標的，開啟全功能圖表，打開pine編輯器
2. 貼上下列程式碼，畫出20、60、120日的雙均線以及抵扣價
```
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/

//@version=4
study("趨勢",overlay=true)
s20 = sma(close, 20)
e20 = ema(close, 20)
s60 = sma(close, 60)
e60 = ema(close, 60)
s120 = sma(close, 120)
e120 = ema(close, 120)
plot(s20, color=color.black)
plot(s60, color=color.blue)
plot(s120, color=color.maroon)
plot(e20, color=color.black, linewidth=2)
plot(e60, color=color.blue, linewidth=2)
plot(e120, color=color.maroon, linewidth=2)
//抵扣價
cond = barstate.islast
x20 = input(20)
close20 = close[x20]
l = label.new(bar_index-x20, na, tostring(x20)+'抵扣 '+tostring(close[x20]), 
  color=color.orange, 
  textcolor=color.white,
  style=close[x20] > open[x20] ? label.style_labeldown : label.style_labelup, 
  yloc=close[x20] > open[x20] ? yloc.abovebar : yloc.belowbar
  )
label.delete(l[1])

x60 = input(60)
close60 = close[x60]
l2 = label.new(bar_index-x60, na, tostring(x60)+'抵扣 '+tostring(close[x60]), 
  color=color.orange, 
  textcolor=color.white,
  style=close[x60] > open[x60] ? label.style_labeldown : label.style_labelup, 
  yloc=close[x60] > open[x60] ? yloc.abovebar : yloc.belowbar
  )
label.delete(l2[1])

x120 = input(120)
close120 = close[x120]
l3 = label.new(bar_index-x120, na, tostring(x120)+'抵扣 '+tostring(close[x120]), 
  color=color.orange, 
  textcolor=color.white,
  style=close[x120] > open[x120] ? label.style_labeldown : label.style_labelup, 
  yloc=close[x120] > open[x120] ? yloc.abovebar : yloc.belowbar
  )
label.delete(l3[1])
```
3. 儲存並加入圖表
4. 創建一個新的空白pine編輯器，貼上下列程式碼，畫出乖離趨勢
```
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/

//@version=4
study("乖離")
cs = (close-ema(close, 20))/ema(close, 20)*100
sm = (ema(close,20)-ema(close,60))/ema(close,60)*100
m1 = (ema(close,60)-ema(close,120))/ema(close,120)*100
plot(m1,"m1", color.silver, linewidth=3,style=plot.style_histogram)
plot(sm,"sm",color.blue)
plot(cs,"cs", color.black)
```
5. 儲存並加入圖表
