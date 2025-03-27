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

    # by row index
    df.iloc[0]

    # by row label
    df.loc['tom']  # by label if index
    df.loc[1]  # label can be an integer, kinda confusing, see `loc[] vs iloc[]` section!


### loc[] vs iloc[]

Use `iloc[]` for strict position-based indexing.

Use `loc[]` for label-based indexing. Column names are "column labels", but there are "row labels" too.

See the difference:

    df = pd.DataFrame(dict(x=list('abcde')))
    
    # with a "standard" index (0-based), both seem to behave the same:
    df.loc[0]['x'] # 'a'
    df.iloc[0]['x'] # 'a'

    # but change the index, and behavior is a lot different:
    df.index = [55, 17, 0, 8, 12]
    df.iloc[0]['x'] # still 'a'
    df.loc[0]['x'] # 'c'!
    df.loc[55]['x'] # 'a' (55 is tne new label for the first row)

Since `loc[]` is label-based, both row and column can be specified as an index:

    df = pd.DataFrame(dict(x=list('abcde'), y=list('ABCDE'), z=range(5)))
    df.loc[0, 'x'] == df.loc[0]['x']
    df.loc[0, ['x','z']] # Series(dict(x='a', z=0))

To use column labels and `iloc[]`, chained indexing is needed:

    df = pd.DataFrame(dict(x=list('abcde'), y=list('ABCDE'), z=range(5)))
    df.iloc[0]['x'] # 'a'
    df.iloc[0][['x','z']] # Series(dict(x='a', z=0))

Warning! Inclusivity when using ranges is different!

    df = pd.DataFrame(dict(x=list('abcde')))
    df.iloc[:1] # first row
    df.loc[:0]  # first row!
    df.iloc[:0] # empty dataframe


### CSV

    df = pd.read_csv('path/to/file.csv', index_col=False, dtype='string')
    pd.to_csv('path/to/file.csv', index=False)


### For text data use dtype `'string'` not `str`

Using `str` seems to be the same as using `object`. Behaviour is better with `'string'`.

> https://towardsdatascience.com/why-we-need-to-use-pandas-new-string-dtype-instead-of-object-for-textual-data-6fd419842e24
