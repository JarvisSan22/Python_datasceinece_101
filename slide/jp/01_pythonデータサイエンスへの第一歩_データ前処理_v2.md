# Pythonデータサイエンスへの第一歩
## データ前処理とPandas基礎

---

## 📚 本日の学習目標

1. データサイエンスの基本的なワークフローを理解する
2. Pandasを使ったデータ操作の基礎を学ぶ
3. 実データを使った分析手法を習得する
4. データ可視化の基本テクニックを身につける

---

## 🛠️ 必要なツール

```python
# 基本的なデータ分析ツール
import pandas as pd    # データフレーム操作
import numpy as np     # 数値計算

# データ可視化ツール
import matplotlib.pyplot as plt  # グラフ描画
import japanize_matplotlib      # 日本語表示対応
```

---

## 📊 今回のデータセット

### マウナロア観測所CO2データ
- 1958年から現在までの観測データ
- 世界で最も長期的なCO2観測記録
- 地球規模の気候変動研究の基準データ

### データの特徴
- 月次測定値
- 高精度な観測データ
- 季節変動と長期トレンドを含む

---

## 📥 データの読み込み

### 1. データのダウンロード
```python
!wget https://scrippsco2.ucsd.edu/assets/data/atmospheric/stations/in_situ_co2/monthly/monthly_in_situ_co2_mlo.csv
```

### 2. データの読み込み
```python
df = pd.read_csv("monthly_in_situ_co2_mlo.csv",
                 skiprows=64)  # ヘッダー情報をスキップ
```

---

## 🔍 データの基本確認

### データの構造を確認
```python
# 基本情報の表示
df.info()

# 先頭データの確認
df.head()

# 基本統計量
df.describe()
```

---

## 🧹 データクリーニング

### 1. 欠損値の確認
```python
# 欠損値のカウント
df.isnull().sum()
```

### 2. 異常値の処理
```python
# -99.99を欠損値に変換
df.replace(-99.99, np.nan, inplace=True)
```

### 3. 欠損値の除去
```python
# 欠損値を含む行を削除
df.dropna(inplace=True)
```

---

## 📊 基本的な可視化

### 時系列プロット
```python
plt.figure(figsize=(12, 6))
plt.plot(df['Date'], df['CO2'])
plt.title('CO2濃度の推移')
plt.xlabel('年')
plt.ylabel('CO2濃度(PPM)')
plt.grid(True)
```

---

## 📈 季節変動の分析

### 月別の変動
```python
# 箱ひげ図による月別分布
plt.figure(figsize=(12, 6))
df.boxplot(column='CO2', by='Mn')
plt.title('月別CO2濃度分布')
```

### 特徴
- 夏季の濃度低下（光合成活性）
- 冬季の濃度上昇
- 年間サイクルの規則性

---

## 📊 トレンド分析

### 年平均の計算
```python
yearly = df.groupby('Yr')['CO2'].mean()
```

### 線形回帰による傾向分析
```python
a, b = np.polyfit(yearly.index, yearly.values, 1)
print(f"年間増加率: {a:.2f} ppm/年")
```

---

## 🔮 未来予測

### 単純線形予測
```python
future_years = np.arange(1958, 2050)
plt.plot(yearly.index, yearly.values, 'o')
plt.plot(future_years, a * future_years + b, 'r--')
plt.title('CO2濃度の予測トレンド')
```

### 予測の限界
- 単純な線形モデルの制約
- 不確実性の考慮
- 複合要因の影響

---

## 💡 実践的なデータ分析のポイント

1. データの品質確認
   - 欠損値の確認
   - 異常値の検出
   - データ型の確認

2. 適切な前処理
   - 欠損値の処理
   - データ型の変換
   - 異常値の処理

3. 効果的な可視化
   - 目的に合ったグラフ選択
   - 適切なスケール設定
   - 分かりやすい表現

---

## 📝 練習課題

1. 2000年以降のデータ分析
   - トレンド計算
   - 季節変動の分析
   - 予測モデルの作成

2. 追加の可視化
   - 移動平均の計算と表示
   - 年間変動幅の分析
   - 複合グラフの作成

---

## 📚 参考資料

- [Pandas公式ドキュメント](https://pandas.pydata.org/docs/)
- [Matplotlib ギャラリー](https://matplotlib.org/stable/gallery/index.html)
- [スクリップスCO2プログラム](https://scrippsco2.ucsd.edu/)

---

## 🎯 次回予告

### データサイエンスの次のステップ
- より高度なデータ操作
- 統計分析の基礎
- 機械学習への導入