# Pythonデータサイエンスへの第一歩
## データ前処理とPandas基礎

---

## 本日の内容

1. CSVデータの読み込み
2. Pandas Dataframe の基本
3. データの前処理
4. データ可視化の基本

---

## 必要なモジュール

```python
import pandas as pd    # データ処理
import numpy as np     # 数値計算
import matplotlib.pyplot as plt  # 可視化
```

---

## 今回のデータセット

- ハワイのマウナロア天文台のCO2観測データ
- 1958年から現在までの大気中CO2濃度
- 月次データ
- [データソース](https://scrippsco2.ucsd.edu/data/atmospheric_co2/primary_mlo_co2_record.html)

---

## CSVファイルの読み込み

### データの特徴
- ファイル上部に説明文あり
- 複数行のヘッダー

### 読み込み方法
```python
df = pd.read_csv("monthly_in_situ_co2_mlo.csv",
                 skiprows=64,  # 説明文をスキップ
                 names=cleaned_header)  # カラム名を指定
```

---

## Pandas基本操作

- `df.head()` - 最初の数行を表示
- `df.info()` - データ形式の情報
- `df.describe()` - 統計情報
- `df.shape` - データサイズ
- `df.columns` - 列名一覧

---

## データのインデックス操作

```python
# インデックスによる選択
df.iloc[0:30]

# ラベルによる選択
df.loc[0:30, ["Date", "CO2"]]

# 条件による選択
df[df["CO2"] > 400]
```

---

## 欠損値の処理

1. 欠損値の確認
```python
df.isnull().sum()
```

2. 特定値を欠損値に変換
```python
df.replace(-99.99, np.nan, inplace=True)
```

3. 欠損値の削除
```python
df.dropna(inplace=True)
```

---

## データ可視化：Pandasの方法

```python
df.plot(x="Date",
        y="CO2",
        title="CO2濃度の時系列",
        grid=True,
        figsize=(12,6))
```

---

## データ可視化：Matplotlibの方法

```python
plt.figure(figsize=(12,6))
plt.plot(x, y)
plt.title("CO2密度の時系列")
plt.xlabel("日付")
plt.ylabel("濃度(PPM)")
plt.grid(True)
plt.show()
```

---

## 応用：月別変動の分析

- 移動平均の計算
- 季節変動の可視化
- 箱ひげ図による月別分布

```python
df_clean.boxplot(column="Residual",
                by="Mn",
                grid=True)
```

---

## 応用：長期トレンド分析

```python
# 年平均の計算と線形回帰
yearly = df.groupby("Yr")["CO2"].mean()
a, b = np.polyfit(X, Y, 1)

print(f"年間平均の増加率: {a:.2f} ppm/年")
```

---

## まとめ

- CSVファイルの読み込みと前処理
- Pandasの基本操作の習得
- 欠損値への対処方法
- データ可視化の基本テクニック
- 実データを用いた分析演習

---

## 次のステップ

- より複雑なデータの前処理
- 高度な統計分析
- 機械学習への応用
- 複数データセットの結合と分析