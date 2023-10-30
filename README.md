# Combining DataFrames With Pandas - Lab

## Introduction

In this lab, you'll gain practice combining DataFrames through concatenation.  You'll also practice executing various types of joins to selectively combine the information stored in the tables.

## Objectives

In this lab you will:

- Use concatenation to combine DataFrames  
- Determine which type of join is preferred for two tables of data and a task  
- Use different types of joins to merge dataframes


## Concatenating DataFrames

Run the cell below to create some sample DataFrames for us to work with.  


```python
import pandas as pd
df1 = pd.DataFrame({'A': ['A0', 'A1', 'A2', 'A3'],
                    'B': ['B0', 'B1', 'B2', 'B3'],
                    'C': ['C0', 'C1', 'C2', 'C3'],
                    'D': ['D0', 'D1', 'D2', 'D3']},
                    index=[0, 1, 2, 3])


df2 = pd.DataFrame({'A': ['A4', 'A5', 'A6', 'A7'],
                    'B': ['B4', 'B5', 'B6', 'B7'],
                    'C': ['C4', 'C5', 'C6', 'C7'],
                    'D': ['D4', 'D5', 'D6', 'D7']},
                    index=[4, 5, 6, 7])

df3 = pd.DataFrame({'A': ['A8', 'A9', 'A10', 'A11'],
                    'B': ['B8', 'B9', 'B10', 'B11'],
                    'C': ['C8', 'C9', 'C10', 'C11'], 
                    'D': ['D8', 'D9', 'D10', 'D11']},
                    index=[8, 9, 10, 11])
```


```python
# __SOLUTION__ 
import pandas as pd
df1 = pd.DataFrame({'A': ['A0', 'A1', 'A2', 'A3'],
                    'B': ['B0', 'B1', 'B2', 'B3'],
                    'C': ['C0', 'C1', 'C2', 'C3'],
                    'D': ['D0', 'D1', 'D2', 'D3']},
                    index=[0, 1, 2, 3])


df2 = pd.DataFrame({'A': ['A4', 'A5', 'A6', 'A7'],
                    'B': ['B4', 'B5', 'B6', 'B7'],
                    'C': ['C4', 'C5', 'C6', 'C7'],
                    'D': ['D4', 'D5', 'D6', 'D7']},
                    index=[4, 5, 6, 7])

df3 = pd.DataFrame({'A': ['A8', 'A9', 'A10', 'A11'],
                    'B': ['B8', 'B9', 'B10', 'B11'],
                    'C': ['C8', 'C9', 'C10', 'C11'], 
                    'D': ['D8', 'D9', 'D10', 'D11']},
                    index=[8, 9, 10, 11])
```

Now that you have multiple DataFrames to work with, you can execute a concatenation to join them together.  

In the cell below, concatenate the 3 DataFrames together using the appropriate function.   


```python
combined_df = None
```


```python
# __SOLUTION__ 
combined_df = pd.concat([df1, df2, df3])
combined_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0</td>
      <td>B0</td>
      <td>C0</td>
      <td>D0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A1</td>
      <td>B1</td>
      <td>C1</td>
      <td>D1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A2</td>
      <td>B2</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A3</td>
      <td>B3</td>
      <td>C3</td>
      <td>D3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A4</td>
      <td>B4</td>
      <td>C4</td>
      <td>D4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>A5</td>
      <td>B5</td>
      <td>C5</td>
      <td>D5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>A6</td>
      <td>B6</td>
      <td>C6</td>
      <td>D6</td>
    </tr>
    <tr>
      <th>7</th>
      <td>A7</td>
      <td>B7</td>
      <td>C7</td>
      <td>D7</td>
    </tr>
    <tr>
      <th>8</th>
      <td>A8</td>
      <td>B8</td>
      <td>C8</td>
      <td>D8</td>
    </tr>
    <tr>
      <th>9</th>
      <td>A9</td>
      <td>B9</td>
      <td>C9</td>
      <td>D9</td>
    </tr>
    <tr>
      <th>10</th>
      <td>A10</td>
      <td>B10</td>
      <td>C10</td>
      <td>D10</td>
    </tr>
    <tr>
      <th>11</th>
      <td>A11</td>
      <td>B11</td>
      <td>C11</td>
      <td>D11</td>
    </tr>
  </tbody>
</table>
</div>



**_EXPECTED OUTPUT:_**

<img src="images/er1.png">

## Setting join conditions with concatenation

You can also specify if the concatenation is an **_Outer Join_** or an **_Inner Join_**.  Next, you'll execute an inner join. Before you do, you need to create another table that contains some overlapping index values with a DataFrame that already exists. 

Run the cell below to create the new DataFrame.


```python
df4 = pd.DataFrame({'B': ['B2', 'B3', 'B6', 'B7'],
                    'D': ['D2', 'D3', 'D6', 'D7'],
                    'F': ['F2', 'F3', 'F6', 'F7']},
                    index=[2, 3, 6, 7])
```


```python
# __SOLUTION__ 
df4 = pd.DataFrame({'B': ['B2', 'B3', 'B6', 'B7'],
                    'D': ['D2', 'D3', 'D6', 'D7'],
                    'F': ['F2', 'F3', 'F6', 'F7']},
                    index=[2, 3, 6, 7])
```

Now, in the cell below, use the `pd.concat()` function to join DataFrames 1 and 4.  However, this time, specify that the `join` is `'inner'`, and `axis=1`. 


```python
df1_and_4 = None
df1_and_4
```


```python
# __SOLUTION__ 
df1_and_4 = pd.concat([df1, df4], axis=1, join='inner')
df1_and_4
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>B</th>
      <th>D</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>A2</td>
      <td>B2</td>
      <td>C2</td>
      <td>D2</td>
      <td>B2</td>
      <td>D2</td>
      <td>F2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A3</td>
      <td>B3</td>
      <td>C3</td>
      <td>D3</td>
      <td>B3</td>
      <td>D3</td>
      <td>F3</td>
    </tr>
  </tbody>
</table>
</div>



**_EXPECTED OUTPUT:_**

<img src='images/er2.png'>

You'll notice that in this case, the results contain only the rows with indexes that exist in both tables -- rows 2 and 3.  The resulting table contains the values for each column in both tables for the rows.  

Note that there are many, many ways that you can make full use of the `pd.concat()` function in pandas to join DataFrames together -- these are just a few of the most common examples pulled from the pandas documentation on the subject. For a full view of all the ways you can use `pd.concat()`, see the [pandas documentation](http://pandas.pydata.org/pandas-docs/stable/merging.html).

## Load data
Now, it's time to move on to working with the Hearthstone cards database.  This database contains information on cards from the popular game, [Hearthstone](https://playhearthstone.com/en-us/). For full information on the dataset, see the [Kaggle page](https://www.kaggle.com/jeradrose/hearthstone-cards) for this dataset. 

This database consists of the following tables:

* _cards_
* *dust_costs*
* _entourages_
* _mechanics_
* *play_requirements*

Many of rows in each table -- but not all -- correspond to the same cards. As such, each table contains a column called `card_id` which acts as a **_Primary Key_** for each table.  You'll make use of these keys to **_join_** the different tables together into a single DataFrame. You'll also experiment with different types of joins to help us decide exactly what information you wish to combine.  

Simply run the cell below to import the tables from the database as DataFrames.


```python
cards_df = pd.read_csv('cards.csv')
dust_df = pd.read_csv('dust.csv')
entourages_df = pd.read_csv('entourages.csv')
mechanics_df = pd.read_csv('mechanics.csv')
play_requirements_df = pd.read_csv('play_requirements.csv')
```


```python
# __SOLUTION__ 
cards_df = pd.read_csv('cards.csv')
dust_df = pd.read_csv('dust.csv')
entourages_df = pd.read_csv('entourages.csv')
mechanics_df = pd.read_csv('mechanics.csv')
play_requirements_df = pd.read_csv('play_requirements.csv')
```

Great.  Now, let's set the correct column, `card_id`, as the index column for each of these tables, and then display each to ensure that everything is as expected.  

For each of the DataFrames you created in the cell above, call the `.set_index()` method and pass in `card_id`.  Also set `inplace=True`.  Then, display the `.head()` of each respective DataFrame to ensure everything worked.  

**_NOTE:_** Since you are performing this operation in place, running any cell a second time will result in pandas throwing an error.  If you need to run something a second time, restart the kernel using the jupyter notebook menu at the top of the page.  


```python

```


```python

```


```python

```


```python

```


```python
# __SOLUTION__ 
cards_df.set_index('card_id', inplace=True)
cards_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>player_class</th>
      <th>type</th>
      <th>name</th>
      <th>set</th>
      <th>text</th>
      <th>cost</th>
      <th>attack</th>
      <th>health</th>
      <th>rarity</th>
      <th>collectible</th>
      <th>flavor</th>
      <th>race</th>
      <th>how_to_earn</th>
      <th>how_to_earn_golden</th>
      <th>targeting_arrow_text</th>
      <th>faction</th>
      <th>durability</th>
    </tr>
    <tr>
      <th>card_id</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>KARA_00_07</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Astral Portal</td>
      <td>KARA</td>
      <td>Summon a random &lt;b&gt;Legendary&lt;/b&gt; minion.</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>NEW1_008a</th>
      <td>DRUID</td>
      <td>SPELL</td>
      <td>Ancient Teachings</td>
      <td>EXPERT1</td>
      <td>Draw a card.</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>BRM_010t2</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Druid of the Flame</td>
      <td>BRM</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>5.0</td>
      <td>COMMON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BEAST</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>AT_132</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Justicar Trueheart</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Replace your starting Hero P...</td>
      <td>6.0</td>
      <td>6.0</td>
      <td>3.0</td>
      <td>LEGENDARY</td>
      <td>1.0</td>
      <td>It's like putting racing stripes and a giant s...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>OG_141</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Faceless Behemoth</td>
      <td>OG</td>
      <td>NaN</td>
      <td>10.0</td>
      <td>10.0</td>
      <td>10.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>Rejected names: Forty-Foot Faceless, Big ol' N...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# __SOLUTION__ 
dust_df.set_index('card_id', inplace=True)
dust_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>action</th>
      <th>cost</th>
    </tr>
    <tr>
      <th>card_id</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BRM_010t2</th>
      <td>CRAFTING_NORMAL</td>
      <td>40</td>
    </tr>
    <tr>
      <th>BRM_010t2</th>
      <td>CRAFTING_GOLDEN</td>
      <td>400</td>
    </tr>
    <tr>
      <th>BRM_010t2</th>
      <td>DISENCHANT_NORMAL</td>
      <td>5</td>
    </tr>
    <tr>
      <th>BRM_010t2</th>
      <td>DISENCHANT_GOLDEN</td>
      <td>50</td>
    </tr>
    <tr>
      <th>AT_132</th>
      <td>CRAFTING_NORMAL</td>
      <td>1600</td>
    </tr>
  </tbody>
</table>
</div>




```python
# __SOLUTION__ 
entourages_df.set_index('card_id', inplace=True)
entourages_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>entourage_card_id</th>
    </tr>
    <tr>
      <th>card_id</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>KAR_A10_22</th>
      <td>KAR_A10_09</td>
    </tr>
    <tr>
      <th>KAR_A10_22</th>
      <td>KAR_A10_02</td>
    </tr>
    <tr>
      <th>KAR_A10_22</th>
      <td>KAR_A10_08</td>
    </tr>
    <tr>
      <th>KAR_A10_22</th>
      <td>KAR_A10_04</td>
    </tr>
    <tr>
      <th>KAR_A10_22</th>
      <td>KAR_A10_05</td>
    </tr>
  </tbody>
</table>
</div>




```python
# __SOLUTION__ 
mechanics_df.set_index('card_id', inplace=True)
mechanics_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>mechanic</th>
    </tr>
    <tr>
      <th>card_id</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>AT_132</th>
      <td>BATTLECRY</td>
    </tr>
    <tr>
      <th>GVG_011a</th>
      <td>TAG_ONE_TURN_EFFECT</td>
    </tr>
    <tr>
      <th>EX1_583</th>
      <td>BATTLECRY</td>
    </tr>
    <tr>
      <th>LOE_007t</th>
      <td>EVIL_GLOW</td>
    </tr>
    <tr>
      <th>LOE_007t</th>
      <td>ImmuneToSpellpower</td>
    </tr>
  </tbody>
</table>
</div>




```python
# __SOLUTION__ 
play_requirements_df.set_index('card_id', inplace=True)
play_requirements_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>play_requirement</th>
      <th>value</th>
    </tr>
    <tr>
      <th>card_id</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>KARA_00_07</th>
      <td>REQ_NUM_MINION_SLOTS</td>
      <td>1</td>
    </tr>
    <tr>
      <th>PRO_001a</th>
      <td>REQ_NUM_MINION_SLOTS</td>
      <td>1</td>
    </tr>
    <tr>
      <th>NAX1_01</th>
      <td>REQ_NUM_MINION_SLOTS</td>
      <td>1</td>
    </tr>
    <tr>
      <th>DS1h_292_H1</th>
      <td>REQ_STEADY_SHOT</td>
      <td>0</td>
    </tr>
    <tr>
      <th>DS1h_292_H1</th>
      <td>REQ_MINION_OR_ENEMY_HERO</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



## Executing Joins

Now that you have the tables loaded correctly, we're going to execute some joins. There are four different kinds of joins, which can best be visualized with Venn diagrams:

<img src='images/Image_198_joins.png'>

In these diagrams, each circle represents a DataFrame or SQL Table. The left table is the table you are working with, and the right table is the table you want to join to the table you are working with. You'll start by executing the most common type of join, an **_Inner Join_**.

In the cell below, join `cards_df` with `mechanics_df` using the built-in `.join()` method on the `cards_df` object. 

Pass in the following parameters:
* the table you want to join with, `mechanics_df`
* The `how` parameter set to the type of join you want, `'inner'`


```python
cards_with_mechanics_df = None
cards_with_mechanics_df
```


```python
# __SOLUTION__ 
cards_with_mechanics_df = cards_df.join(mechanics_df, how='inner')
cards_with_mechanics_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>player_class</th>
      <th>type</th>
      <th>name</th>
      <th>set</th>
      <th>text</th>
      <th>cost</th>
      <th>attack</th>
      <th>health</th>
      <th>rarity</th>
      <th>collectible</th>
      <th>flavor</th>
      <th>race</th>
      <th>how_to_earn</th>
      <th>how_to_earn_golden</th>
      <th>targeting_arrow_text</th>
      <th>faction</th>
      <th>durability</th>
      <th>mechanic</th>
    </tr>
    <tr>
      <th>card_id</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>AT_002</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Effigy</td>
      <td>TGT</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When a friendly minion dies, su...</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>Burning man, brah.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>SECRET</td>
    </tr>
    <tr>
      <th>AT_005t</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Boar</td>
      <td>TGT</td>
      <td>&lt;b&gt;Charge&lt;/b&gt;</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BEAST</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CHARGE</td>
    </tr>
    <tr>
      <th>AT_006</th>
      <td>MAGE</td>
      <td>MINION</td>
      <td>Dalaran Aspirant</td>
      <td>TGT</td>
      <td>&lt;b&gt;Inspire:&lt;/b&gt; Gain &lt;b&gt;Spell Damage +1&lt;/b&gt;.</td>
      <td>4.0</td>
      <td>3.0</td>
      <td>5.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>Is he aspiring or inspiring?  Make up your mind!</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>INSPIRE</td>
    </tr>
    <tr>
      <th>AT_007</th>
      <td>MAGE</td>
      <td>MINION</td>
      <td>Spellslinger</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Add a random spell to each p...</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>Does he sling spells, or do his spells linger ...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BATTLECRY</td>
    </tr>
    <tr>
      <th>AT_009</th>
      <td>MAGE</td>
      <td>MINION</td>
      <td>Rhonin</td>
      <td>TGT</td>
      <td>&lt;b&gt;Deathrattle:&lt;/b&gt; Add 3 copies of Arcane Mis...</td>
      <td>8.0</td>
      <td>7.0</td>
      <td>7.0</td>
      <td>LEGENDARY</td>
      <td>1.0</td>
      <td>A masterless shamurai.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DEATHRATTLE</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>XXX_105</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Add 8 to Health.</td>
      <td>CHEAT</td>
      <td>Adds 8 health to a damaged character. Does NOT...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>COMMON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>ImmuneToSpellpower</td>
    </tr>
    <tr>
      <th>XXX_107</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Set Health to 1</td>
      <td>CHEAT</td>
      <td>Set a character's health to 1, and remove all ...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>COMMON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>ImmuneToSpellpower</td>
    </tr>
    <tr>
      <th>XXX_110</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Yogg-Saron Test (Auto)</td>
      <td>CHEAT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Cast 30 random spells &lt;i&gt;(ta...</td>
      <td>0.0</td>
      <td>7.0</td>
      <td>5.0</td>
      <td>LEGENDARY</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BATTLECRY</td>
    </tr>
    <tr>
      <th>hexfrog</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Frog</td>
      <td>CORE</td>
      <td>&lt;b&gt;Taunt&lt;/b&gt;</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>COMMON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BEAST</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>TAUNT</td>
    </tr>
    <tr>
      <th>tt_010</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Spellbender</td>
      <td>EXPERT1</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When an enemy casts a spell on ...</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>EPIC</td>
      <td>1.0</td>
      <td>While it's fun to intercept enemy lightning bo...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>SECRET</td>
    </tr>
  </tbody>
</table>
<p>1079 rows × 18 columns</p>
</div>



Examine the output from the cell above and compare it to the original output of both the `cards_df` and `mechanics_df` DataFrame heads you displayed earlier.  Notice how this now combines the columns from both?

**_Question_**

If you inspect the original `cards_df` DataFrame, you'll notice that it contains  2,819 records.  The result of our inner join, `cards_with_mechanics_df`, contains only 1079 rows.  Why?

Write your answer below this line:
________________________________________________________________________________

<details>
    <summary style="cursor: pointer; display: inline">
        <b><u>Solution (click to reveal)</u></b>
    </summary>
    <p>First we performed an inner join, which only includes records that are present in both tables. Although there were 2819 records in the left table, there were only 1079 records that existed in both tables, which are what you see in the resulting dataframe. </p>
</details>

## Other Types of Joins

By default, the `.join()` method performs a left join if no parameter is passed in for `how=`.  In the cell below, perform a **_Left Join_** of `cards_with_mechanics_df` and `play_requirements_df`, with `cards_with_mechanics_df` as the left table.  

Then, display `left_join_df` to inspect our results. 


```python
left_join_df = None
left_join_df
```


```python
# __SOLUTION__ 
left_join_df = cards_with_mechanics_df.join(play_requirements_df)
left_join_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>player_class</th>
      <th>type</th>
      <th>name</th>
      <th>set</th>
      <th>text</th>
      <th>cost</th>
      <th>attack</th>
      <th>health</th>
      <th>rarity</th>
      <th>collectible</th>
      <th>flavor</th>
      <th>race</th>
      <th>how_to_earn</th>
      <th>how_to_earn_golden</th>
      <th>targeting_arrow_text</th>
      <th>faction</th>
      <th>durability</th>
      <th>mechanic</th>
      <th>play_requirement</th>
      <th>value</th>
    </tr>
    <tr>
      <th>card_id</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>AT_002</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Effigy</td>
      <td>TGT</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When a friendly minion dies, su...</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>Burning man, brah.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>SECRET</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>AT_005t</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Boar</td>
      <td>TGT</td>
      <td>&lt;b&gt;Charge&lt;/b&gt;</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BEAST</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CHARGE</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>AT_006</th>
      <td>MAGE</td>
      <td>MINION</td>
      <td>Dalaran Aspirant</td>
      <td>TGT</td>
      <td>&lt;b&gt;Inspire:&lt;/b&gt; Gain &lt;b&gt;Spell Damage +1&lt;/b&gt;.</td>
      <td>4.0</td>
      <td>3.0</td>
      <td>5.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>Is he aspiring or inspiring?  Make up your mind!</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>INSPIRE</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>AT_007</th>
      <td>MAGE</td>
      <td>MINION</td>
      <td>Spellslinger</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Add a random spell to each p...</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>Does he sling spells, or do his spells linger ...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BATTLECRY</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>AT_009</th>
      <td>MAGE</td>
      <td>MINION</td>
      <td>Rhonin</td>
      <td>TGT</td>
      <td>&lt;b&gt;Deathrattle:&lt;/b&gt; Add 3 copies of Arcane Mis...</td>
      <td>8.0</td>
      <td>7.0</td>
      <td>7.0</td>
      <td>LEGENDARY</td>
      <td>1.0</td>
      <td>A masterless shamurai.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DEATHRATTLE</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>XXX_105</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Add 8 to Health.</td>
      <td>CHEAT</td>
      <td>Adds 8 health to a damaged character. Does NOT...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>COMMON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>ImmuneToSpellpower</td>
      <td>REQ_TARGET_TO_PLAY</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>XXX_107</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Set Health to 1</td>
      <td>CHEAT</td>
      <td>Set a character's health to 1, and remove all ...</td>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>COMMON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>ImmuneToSpellpower</td>
      <td>REQ_TARGET_TO_PLAY</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>XXX_110</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Yogg-Saron Test (Auto)</td>
      <td>CHEAT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Cast 30 random spells &lt;i&gt;(ta...</td>
      <td>0.0</td>
      <td>7.0</td>
      <td>5.0</td>
      <td>LEGENDARY</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BATTLECRY</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>hexfrog</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Frog</td>
      <td>CORE</td>
      <td>&lt;b&gt;Taunt&lt;/b&gt;</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>COMMON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BEAST</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>TAUNT</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>tt_010</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Spellbender</td>
      <td>EXPERT1</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When an enemy casts a spell on ...</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>EPIC</td>
      <td>1.0</td>
      <td>While it's fun to intercept enemy lightning bo...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>SECRET</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>1226 rows × 20 columns</p>
</div>



Note that the results of this sort of join are dependent upon the position of each table--if you were to make `cards_with_mechanics_df` the right table and `play_requirements_df` the left table and then perform a **_Right Join_**, our results would be the same. 

**_Question:_**

Describe what was included from each table in this join.

Write your answer below this line:
________________________________________________________________________________

<details>
    <summary style="cursor: pointer; display: inline">
        <b><u>Solution (click to reveal)</u></b>
    </summary>
    <p>Every record from cards_with_mechanics_df, as well as any records from play_requirements_df that have matching index values with a record from the left table. </p>
</details>

#### Outer Joins

In the cell below, perform an outer join between `cards_df` and `dust_df`. Since these tables contain columns with the same name, we'll need to specify a suffix for at least one of them, so that the column can be renamed to avoid a naming collision. 

During this join, set the `rsuffix` parameter to `_dust`


```python
outer_join_df = None
outer_join_df
```


```python
# __SOLUTION__ 
outer_join_df = cards_df.join(dust_df, rsuffix='_dust', how='outer')
outer_join_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>player_class</th>
      <th>type</th>
      <th>name</th>
      <th>set</th>
      <th>text</th>
      <th>cost</th>
      <th>attack</th>
      <th>health</th>
      <th>rarity</th>
      <th>collectible</th>
      <th>flavor</th>
      <th>race</th>
      <th>how_to_earn</th>
      <th>how_to_earn_golden</th>
      <th>targeting_arrow_text</th>
      <th>faction</th>
      <th>durability</th>
      <th>action</th>
      <th>cost_dust</th>
    </tr>
    <tr>
      <th>card_id</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>AT_001</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Flame Lance</td>
      <td>TGT</td>
      <td>Deal $8 damage to a minion.</td>
      <td>5.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>It's on the rack next to ice lance, acid lance...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CRAFTING_NORMAL</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>AT_001</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Flame Lance</td>
      <td>TGT</td>
      <td>Deal $8 damage to a minion.</td>
      <td>5.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>It's on the rack next to ice lance, acid lance...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CRAFTING_GOLDEN</td>
      <td>400.0</td>
    </tr>
    <tr>
      <th>AT_001</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Flame Lance</td>
      <td>TGT</td>
      <td>Deal $8 damage to a minion.</td>
      <td>5.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>It's on the rack next to ice lance, acid lance...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DISENCHANT_NORMAL</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>AT_001</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Flame Lance</td>
      <td>TGT</td>
      <td>Deal $8 damage to a minion.</td>
      <td>5.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>It's on the rack next to ice lance, acid lance...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DISENCHANT_GOLDEN</td>
      <td>50.0</td>
    </tr>
    <tr>
      <th>AT_002</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Effigy</td>
      <td>TGT</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When a friendly minion dies, su...</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>Burning man, brah.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CRAFTING_NORMAL</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>tt_010</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Spellbender</td>
      <td>EXPERT1</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When an enemy casts a spell on ...</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>EPIC</td>
      <td>1.0</td>
      <td>While it's fun to intercept enemy lightning bo...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DISENCHANT_GOLDEN</td>
      <td>400.0</td>
    </tr>
    <tr>
      <th>tt_010a</th>
      <td>MAGE</td>
      <td>MINION</td>
      <td>Spellbender</td>
      <td>EXPERT1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>EPIC</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CRAFTING_NORMAL</td>
      <td>400.0</td>
    </tr>
    <tr>
      <th>tt_010a</th>
      <td>MAGE</td>
      <td>MINION</td>
      <td>Spellbender</td>
      <td>EXPERT1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>EPIC</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CRAFTING_GOLDEN</td>
      <td>1600.0</td>
    </tr>
    <tr>
      <th>tt_010a</th>
      <td>MAGE</td>
      <td>MINION</td>
      <td>Spellbender</td>
      <td>EXPERT1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>EPIC</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DISENCHANT_NORMAL</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>tt_010a</th>
      <td>MAGE</td>
      <td>MINION</td>
      <td>Spellbender</td>
      <td>EXPERT1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>EPIC</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DISENCHANT_GOLDEN</td>
      <td>400.0</td>
    </tr>
  </tbody>
</table>
<p>5849 rows × 19 columns</p>
</div>



Inspect the output above.  Note that the naming collision has been avoided by renaming the `cost` column from the right table to `cost_dust`.  

## Summary

In this lab, you learned how to:

* Concatenate multiple DataFrames together into a single DataFrame
* Understand and execute the various types of joins (inner, outer, left, and right joins)
