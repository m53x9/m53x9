
//m53x9
//mustafaFx
//@version=5
indicator(title="hmaFx", shorttitle="hmaFx", overlay=true, timeframe="", timeframe_gaps=true)
length = input.int(61, minval=1)
src = input(close, title="Source")
hma = ta.wma(2*ta.wma(src, length/2)-ta.wma(src, length), math.floor(math.sqrt(length)))
plot(hma,color=ta.falling(hma,1)?color.red:color.green)

//macdFx

[m,s,h] = ta.macd(close,12,26,9)
plotshape(ta.crossunder(m,s),color=color.red)
plotshape(ta.crossover(m,s),color=color.green)

/////////////////////////////////////////////////////////////////////supertrend

atrPeriod = input(10, "ATR Length")
factor = input.float(3.0, "Factor", step = 0.01)

[supertrend, direction] = ta.supertrend(factor, atrPeriod)

bodyMiddle = plot((open + close) / 2, display=display.none)
upTrend = plot(direction < 0 ? supertrend : na, "Up Trend", color = color.green, style=plot.style_linebr)
downTrend = plot(direction < 0? na : supertrend, "Down Trend", color = color.red, style=plot.style_linebr)

fill(bodyMiddle, upTrend, color.new(color.green, 90), fillgaps=false)
fill(bodyMiddle, downTrend, color.new(color.red, 90), fillgaps=false)

/////000000000000000000000000000000000000000000000000000smooth sma
len = input.int(21, minval=1, title="Length")
srcs = input(close, title="Source")
smma = 0.0
smma := na(smma[1]) ? ta.sma(srcs, len) : (smma[1] * (len - 1) + srcs) / len
plot(smma, color=#673AB7)

lenx = input.int(50, minval=1, title="Length")
srcsx = input(close, title="Source")
smmax = 0.0
smmax := na(smmax[2]) ? ta.sma(srcsx, lenx) : (smmax[2] * (len - 1) + srcsx) / len
plot(smmax, color=#673AB7)
