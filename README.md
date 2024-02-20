### SonolusScoreCalc.
## 計算方法
# スコア計算
score = (perfect数×1.01 + great数×1.00 + good数×0.5) × (1000000÷総ノーツ数)

# 単曲レート計算
threshold=各ランクの下限, rank=ランク, base=下限値でのベースからのレート上昇分, diff=このスコアごとにレートが0.01上がる
{ threshold: 1009000, rank: 'SSS+' , base: 2.15, diff: 10000},
{ threshold: 1007500, rank: 'SSS' , base: 2.00, diff: 100},
{ threshold: 1005000, rank: 'SS+' , base: 1.50, diff: 50},
{ threshold: 1000000, rank: 'SS' , base: 1.00, diff: 100},
{ threshold: 990000, rank: 'S+' , base: 0.60, diff: 250},
{ threshold: 975000, rank: 'S' , base: 0.00, diff: 250},
{ threshold: 950000, rank: 'AAA' , base: -1.50, diff: 166.67},
{ threshold: 925000, rank: 'AA' , base: -3.00, diff: 166.67},
{ threshold: 900000, rank: 'A' , base: -5.00, diff: 125},
{ threshold: 800000, rank: 'BBB' , base: -10.00, diff: 10000},
{ threshold: 700000, rank: 'BB' , base: -15.00, diff: 10000},
{ threshold: 600000, rank: 'B' , base: -20.00, diff: 10000},
{ threshold: 500000, rank: 'C' , base: -25.00, diff: 10000},
{ threshold: 0, rank: 'D' , base: -99.00, diff: 10000}

譜面定数をchunithm基準に変換. chunithmの15がsonolusの36.0に, chunithmの14がsonolusの31.0に相当
chunithm_rate=((15-14)/(36-31))*(sonolus_rate-31)+14;

レートを計算
rate = 譜面定数 + base + ((score - threshold)/diff)*0.01

譜面定数をsonolus基準に逆変換し、1.2倍する
sonolus_rate=(((36-31)/(15-14))*(chunithm_rate-14)+31)*1.2

# 総合レート計算
単曲レートが最も高いもの最大10個を計算対象とする.
rate_avg = (レート対象曲の単曲レートの合計/10)*0.75 + (単曲レート1位の曲の単曲レート値)*0.25
