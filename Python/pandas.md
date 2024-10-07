# pandas library

## Matching dplyr commands in pandas

[Here](https://pandas.pydata.org/docs/getting_started/comparison/comparison_with_r.html)

## data frame indexing

- `df.loc`: label indexing (column/row names)
- `df.iloc`: number indexing (column/row numbers)

## Query

- `df.query('A== 3')`:  find matches in the data frame

## agg

`aa_scores_pd.agg(['min','max'],axis=0)`: get max and min of each column
`aa_scores_pd.agg(['min','max'],axis=1)`: get max and min of each row