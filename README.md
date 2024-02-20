# SonolusScoreCalc.
## 計算方法
### スコア計算
score = (perfect数×1.01 + great数×1.00 + good数×0.5) × (1000000÷総ノーツ数)

### 単曲レート計算
```
threshold=各ランクの下限
rank=ランク
base=下限値でのベースからのレート上昇分
diff=このスコアごとにレートが0.01上がる
```
#### Rank Thresholds

- **SSS+**: 1,009,000 points (Base: 2.15, Diff: 10,000)
- **SSS**: 1,007,500 points (Base: 2.00, Diff: 100)
- **SS+**: 1,005,000 points (Base: 1.50, Diff: 50)
- **SS**: 1,000,000 points (Base: 1.00, Diff: 100)
- **S+**: 990,000 points (Base: 0.60, Diff: 250)
- **S**: 975,000 points (Base: 0.00, Diff: 250)
- **AAA**: 950,000 points (Base: -1.50, Diff: 166.67)
- **AA**: 925,000 points (Base: -3.00, Diff: 166.67)
- **A**: 900,000 points (Base: -5.00, Diff: 125)
- **BBB**: 800,000 points (Base: -10.00, Diff: 10,000)
- **BB**: 700,000 points (Base: -15.00, Diff: 10,000)
- **B**: 600,000 points (Base: -20.00, Diff: 10,000)
- **C**: 500,000 points (Base: -25.00, Diff: 10,000)
- **D**: 0 points (Base: -99.00, Diff: 10,000)


譜面定数をchunithm基準に変換. chunithmの15がsonolusの36.0に, chunithmの14がsonolusの31.0に相当
```
chunithm_rate=((15-14)/(36-31))*(sonolus_rate-31)+14;
```

レートを計算
```
rate = 譜面定数 + base + ((score - threshold)/diff)*0.01
```

譜面定数をsonolus基準に逆変換し、1.2倍する
```
sonolus_rate=(((36-31)/(15-14))*(chunithm_rate-14)+31)*1.2
```

### 総合レート計算
単曲レートが最も高いもの最大10個を計算対象とする.
```
rate_avg = (レート対象曲の単曲レートの合計/10)*0.75 + (単曲レート1位の曲の単曲レート値)*0.25
```
