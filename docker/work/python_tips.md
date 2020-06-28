## dataframe
```python
df.dtypes
df=['col1'].str #要素にはstrでアクセスできる
df=['col1'].astype('str') #型変換

pd.to_datetime(df['col1']) #strからdatetime64へ
df['col1dt'].dt # dtでアクセス
df.sort_values('col1') # 日本語ソートはできない

df[df['col1'] > 1] #boolean indexingで抽出
df.query('col1 == "1"')#queryで抽出
df.query('col1 > @higher') #変数は@つける

df.shift()#一行ずらす
df.shift(3, axis=1)#横に3つずらす

df[df.duplicated(subset='col1')] # booleanSeriesで抽出できる
df.drop_duplicates(subset=['col1', 'col2'], inplace=True) # inplaceTrueで元dfを編集する

df.mean() #dataframeは計算メソッドを持っている
df['col1'].sum() #seriesでもおk

df.dropna() # NaNある行を削除
df.drop_duplicates('col1', inplace=True) #重複を削除
df.sample(n=5)# ランダムに引数の値行を取得

df.isnull().values.sum() # numpy.ndarrayのsumはデフォで全体の合計を算出

df.groupby('col1').agg({'col2':'min'})
df.groupby('col1').apply(lambda x: x**2)
df.groupby('col1').apply(lambda x: some(x)) # 一般の関数はapplyで当てる
df.groupby(['col1, col2'])
# https://pandas.pydata.org/pandas-docs/stable/reference/groupby.html

df.merge(t1, t2, on='key1', how='inner')
# sql select相当はないので、結合テーブルでカラムを調整する
# how inner/left/right/outer
# left_on/right_onで異なる列名をonする

train_test_split(x, y, test_size=0.2, stratify=y) # 層化(引数に均等に分散させたいラベルを指定)
preprocessing.scale(df['col1']) # 標準分散

df.read_csv('data/in.csv')# その他パラメータは大体下と一緒
pd.to_csv('data/out.csv', header=None, encoding='CP932') #初期値:header=True, encoding=utf-8, sep=','
```

## 置換
```python
#series
df['col1'].apply(lambda x: True if x=1 else False) #一行にapplyされる
df['col1'].map({'1':True, '0':False}) #dictのkeyがvalueにmapされる
df['col2'].map('{:.0f}'.format) #整数に丸める

#nan
df.isnull() # 確認
df.dropna() # 消す
df.fillna({'col1': np.nanmean(df['col1'])}) #nan系はnpを使う mean/median
```

## 特定文字列を抽出する
contains/startswith/endswith/matchでqueryする
```python
query('store_cd.str.endswith("1")', engine='python')
query('status_cd.str.contains("^[A-F]")', engine='python')
```
## 正規表現
([0-9]{3}-[0-9]{4}-[0-9]{4}) #電話番号形式
^(?!abc) #abc以外から始まる
## concat
axis=0(デフォルト): 行追加
axis=1:列追加
## groupby obj.agg
aggできるのはmin, max, mean, median, std, count
modeはcol.apply(lambda x: x.mode()

## sklearn
```python
df_train, df_test = train_test_split(df, test_size=0.7)
# random_seedで分割を固定できる
# 変数名を文字列にするにはdictかlist
```

## 不均衡データサンプリング
不正利用のような目的変数が不均衡なデータをpreprocessとして、2つのやり方がある
```python
# 負例を減らす:UnderSampling

# 正例を増やす:OverSampling

```