### Cheat sheet

https://pandas.pydata.org/Pandas_Cheat_Sheet.pdf


### Instantiation

    # using dict of columns
    pd.DataFrame(dict(id=[100, 200, 300], name=['Alice', 'Bob', 'Charlie']))

    # using dicts aka 'records'
    pd.DataFrame([dict(id=100, name='Alice'), dict(id=200, name='Bob'), dict(id=300, name='Charlie')])

    # using a list or any iterable. the index will be integers
    pd.Series([1, 2, 3, 4])

    # using a dict. the indicies will be the dict keys
    pd.Series(dict(name='derp', size=5))

    # allocating a specific size
    pd.Series(None, dtype='string', index=range(len(df)))


### Access

    # by column
    df['First Name']
    df.Address  # or dot notation for single-word column name

    # by row
    df.iloc[0]
    df.iloc['tom']  # by label if index


### CSV

    df = pd.read_csv('path/to/file.csv', index_col=False, dtype='string')
    pd.to_csv('path/to/file.csv', index=False)


### For text data use dtype `'string'` not `str`

Using `str` seems to be the same as using `object`. Behaviour is better with `'string'`.

> https://towardsdatascience.com/why-we-need-to-use-pandas-new-string-dtype-instead-of-object-for-textual-data-6fd419842e24
