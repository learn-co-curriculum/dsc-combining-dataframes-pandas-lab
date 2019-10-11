
# Combining DataFrames With Pandas - Lab

## Introduction

In this lab, you'll gain practice combining DataFrames through concatenation.  You'll also practice executing various types of joins to selectively combine the information stored in the tables!

## Objectives

- Concatenate multiple DataFrames together into a single DataFrame
- Understand and execute the various types of joins (inner, outer, left, and right joins)


## Getting Started

You'll start with a quick section to gain practice with concatenating datasets using `pd.concat()`.

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

Now that you have multiple DataFrames to work with, you can execute a concatenation to join them together.  

In the cell below, concatenate the 3 DataFrames together using the appropriate function.   


```python
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

## Setting Join Conditions With Concatenation

You can also specify if the concatenation is an **_Outer Join_** or an **_Inner Join_**.  Next, you'll execute an inner join. Before you do, you need to create another table that contains some overlapping index values with a DataFrame that already exists. 

Run the cell below to create the new DataFrame.


```python
df4 = pd.DataFrame({'B': ['B2', 'B3', 'B6', 'B7'],
                    'D': ['D2', 'D3', 'D6', 'D7'],
                    'F': ['F2', 'F3', 'F6', 'F7']},
                    index=[2, 3, 6, 7])
```

Now, in the cell below, use the `pd.concat()` method to join DataFrames 1 and 4.  However, this time, specify that the `join` is `'inner'`, and `axis=1`. 


```python
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

You'll notice that in this case, the results returned contain only the rows with indexes that exist in both tables--rows 2 and 3.  The resulting table contains the values for each column in both tables for the rows.  

Note that there are many, many ways that you can make full use of the `concat()` functionality in pandas to join DataFrames together--these are just a few of the most common examples pulled from the pandas documentation on the subject.  For a full view of all the ways you can use `pd.concat()`, see the [pandas documentation](http://pandas.pydata.org/pandas-docs/stable/merging.html)!

## Loading In Data
Now, it's time to move on to working with the Hearthstone cards database.  This database contains information on cards from the popular game, [Hearthstone](https://playhearthstone.com/en-us/)! For full information on the dataset, see the  [kaggle page](https://www.kaggle.com/jeradrose/hearthstone-cards) for this dataset. 

This database consists of the following tables:

* _cards_
* *dust_costs*
* _entourages_
* _mechanics_
* *play_requirements*

Many of rows in each table--but not all--correspond to the same cards. As such, each table contains a column called `card_id` which acts as a **_Primary Key_** for each table.  You'll make use of these keys to **_join_** the different tables together into a single DataFrame.  You'll also experiment with different types of joins to help us decide exactly what information you wish to combine.  

Simply run the cell below to import the tables from the database as DataFrames.


```python
cards_df = pd.read_csv('cards.csv')
dust_df = pd.read_csv('dust.csv')
entourages_df = pd.read_csv('entourages.csv')
mechanics_df = pd.read_csv('mechanics.csv')
play_requirements_df = pd.read_csv('play_requirements.csv')
```

Great.  Now, let's set the correct column, `card_id`, as the index column for each of these tables, and then display each to ensure that everything is as expected.  

For each of the dataframes you created in the cell above, call the `.set_index()` method and pass in `card_id`.  Also set `inplace=True`.  Then, display the head of each respective DataFrame to ensure everything worked.  

**_NOTE:_** Since you are performing this operation in place, running any cell a second time will result in pandas throwing an error.  If you need to run something a second time, restart the kernel using the jupyter notebook menu at the top of the page.  


```python
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

Now that you have the tables loaded correctly, we're going to execute some joins. There are 4 different kinds of joins, which can best be visualized with Venn diagrams:

<img src='images/Image_198_joins.png'>

In these diagrams, each circle represents a DataFrame or SQL Table.  The left table is the table you are working with, and the right table is the table you want to join to the table you are working with.  You'll start by executing the most common type of join, an **_Inner Join_**.

In the cell below, join `cards_df` with `mechanics_df` using the built-in `.join()` method on the `cards_df` object. 

Pass in the following parameters:
* the table you want to join with, `mechanics_df`
* The `how` parameter set to the type of join you want, `'inner'`


```python
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
      <th>AT_010</th>
      <td>HUNTER</td>
      <td>MINION</td>
      <td>Ram Wrangler</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; If you have a Beast, summon ...</td>
      <td>5.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>Not getting trampled is really the trick here.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BATTLECRY</td>
    </tr>
    <tr>
      <th>AT_011e</th>
      <td>NEUTRAL</td>
      <td>ENCHANTMENT</td>
      <td>Light's Blessing</td>
      <td>TGT</td>
      <td>Increased Attack.</td>
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
      <td>NaN</td>
      <td>AURA</td>
    </tr>
    <tr>
      <th>AT_012</th>
      <td>PRIEST</td>
      <td>MINION</td>
      <td>Spawn of Shadows</td>
      <td>TGT</td>
      <td>&lt;b&gt;Inspire:&lt;/b&gt; Deal 4 damage to each hero.</td>
      <td>4.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>What did you expect to happen?  He's a Spawn. ...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>INSPIRE</td>
    </tr>
    <tr>
      <th>AT_017</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Twilight Guardian</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; If you're holding a Dragon, ...</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>6.0</td>
      <td>EPIC</td>
      <td>1.0</td>
      <td>A result of magical experiments carried out by...</td>
      <td>DRAGON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BATTLECRY</td>
    </tr>
    <tr>
      <th>AT_018</th>
      <td>PRIEST</td>
      <td>MINION</td>
      <td>Confessor Paletress</td>
      <td>TGT</td>
      <td>&lt;b&gt;Inspire:&lt;/b&gt; Summon a random &lt;b&gt;Legendary&lt;/...</td>
      <td>7.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>LEGENDARY</td>
      <td>1.0</td>
      <td>She sees into your past and makes you face you...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>INSPIRE</td>
    </tr>
    <tr>
      <th>AT_019</th>
      <td>WARLOCK</td>
      <td>MINION</td>
      <td>Dreadsteed</td>
      <td>TGT</td>
      <td>&lt;b&gt;Deathrattle:&lt;/b&gt; Summon a Dreadsteed.</td>
      <td>4.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>EPIC</td>
      <td>1.0</td>
      <td>Crescendo himself summoned this steed, riding ...</td>
      <td>DEMON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DEATHRATTLE</td>
    </tr>
    <tr>
      <th>AT_022</th>
      <td>WARLOCK</td>
      <td>SPELL</td>
      <td>Fist of Jaraxxus</td>
      <td>TGT</td>
      <td>When you play or discard this, deal $4 damage ...</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>* Not actually Jaraxxus' fist.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>InvisibleDeathrattle</td>
    </tr>
    <tr>
      <th>AT_023</th>
      <td>WARLOCK</td>
      <td>MINION</td>
      <td>Void Crusher</td>
      <td>TGT</td>
      <td>&lt;b&gt;Inspire:&lt;/b&gt; Destroy a random minion for ea...</td>
      <td>6.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>We like to call him "Wesley".</td>
      <td>DEMON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>INSPIRE</td>
    </tr>
    <tr>
      <th>AT_028</th>
      <td>ROGUE</td>
      <td>MINION</td>
      <td>Shado-Pan Rider</td>
      <td>TGT</td>
      <td>&lt;b&gt;Combo:&lt;/b&gt; Gain +3 Attack.</td>
      <td>5.0</td>
      <td>3.0</td>
      <td>7.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>He needed a break after that business in the V...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>COMBO</td>
    </tr>
    <tr>
      <th>AT_030</th>
      <td>ROGUE</td>
      <td>MINION</td>
      <td>Undercity Valiant</td>
      <td>TGT</td>
      <td>&lt;b&gt;Combo:&lt;/b&gt; Deal 1 damage.</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>Almost went to play for Stormwind before signi...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Deal 1 damage.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>COMBO</td>
    </tr>
    <tr>
      <th>AT_032</th>
      <td>ROGUE</td>
      <td>MINION</td>
      <td>Shady Dealer</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; If you have a Pirate, gain +...</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>3.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>I have great deal for you... for 4 damage to y...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BATTLECRY</td>
    </tr>
    <tr>
      <th>AT_035t</th>
      <td>ROGUE</td>
      <td>SPELL</td>
      <td>Ambush!</td>
      <td>TGT</td>
      <td>When you draw this, summon a 4/4 Nerubian for ...</td>
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
      <td>TOPDECK</td>
    </tr>
    <tr>
      <th>AT_036</th>
      <td>ROGUE</td>
      <td>MINION</td>
      <td>Anub'arak</td>
      <td>TGT</td>
      <td>&lt;b&gt;Deathrattle:&lt;/b&gt; Return this to your hand a...</td>
      <td>9.0</td>
      <td>8.0</td>
      <td>4.0</td>
      <td>LEGENDARY</td>
      <td>1.0</td>
      <td>Was actually a pretty nice guy before, you kno...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DEATHRATTLE</td>
    </tr>
    <tr>
      <th>AT_037</th>
      <td>DRUID</td>
      <td>SPELL</td>
      <td>Living Roots</td>
      <td>TGT</td>
      <td>&lt;b&gt;Choose One -&lt;/b&gt; Deal $2 damage; or Summon ...</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>2 out of 2 saplings recommend that you summon ...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CHOOSE_ONE</td>
    </tr>
    <tr>
      <th>AT_038</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Darnassus Aspirant</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Gain an empty Mana Crystal.\...</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>She loves mana crystals, she hates mana crysta...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BATTLECRY</td>
    </tr>
    <tr>
      <th>AT_038</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Darnassus Aspirant</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Gain an empty Mana Crystal.\...</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>She loves mana crystals, she hates mana crysta...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DEATHRATTLE</td>
    </tr>
    <tr>
      <th>AT_039</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Savage Combatant</td>
      <td>TGT</td>
      <td>&lt;b&gt;Inspire:&lt;/b&gt; Give your hero\n+2 Attack this...</td>
      <td>4.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>Maybe if you whistle a tune it will soothe him...</td>
      <td>BEAST</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>INSPIRE</td>
    </tr>
    <tr>
      <th>AT_039e</th>
      <td>DRUID</td>
      <td>ENCHANTMENT</td>
      <td>Savage</td>
      <td>TGT</td>
      <td>+2 Attack this turn.</td>
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
      <td>NaN</td>
      <td>TAG_ONE_TURN_EFFECT</td>
    </tr>
    <tr>
      <th>AT_040</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Wildwalker</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Give a friendly Beast +3 Hea...</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>She was born to be something.  She is just not...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BATTLECRY</td>
    </tr>
    <tr>
      <th>AT_042</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Druid of the Saber</td>
      <td>TGT</td>
      <td>&lt;b&gt;Choose One -&lt;/b&gt; Transform to gain &lt;b&gt;Charg...</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>That's saberTEETH, not like curved pirate blad...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CHOOSE_ONE</td>
    </tr>
    <tr>
      <th>AT_042t</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Sabertooth Lion</td>
      <td>TGT</td>
      <td>&lt;b&gt;Charge&lt;/b&gt;</td>
      <td>2.0</td>
      <td>2.0</td>
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
      <td>CHARGE</td>
    </tr>
    <tr>
      <th>AT_042t2</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Sabertooth Panther</td>
      <td>TGT</td>
      <td>&lt;b&gt;Stealth&lt;/b&gt;</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>COMMON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BEAST</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>STEALTH</td>
    </tr>
    <tr>
      <th>AT_045</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Aviana</td>
      <td>TGT</td>
      <td>Your minions cost (1).</td>
      <td>9.0</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>LEGENDARY</td>
      <td>1.0</td>
      <td>Call her "Tweety".  She'll find it real funny....</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>AURA</td>
    </tr>
    <tr>
      <th>AT_046</th>
      <td>SHAMAN</td>
      <td>MINION</td>
      <td>Tuskarr Totemic</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Summon a random basic Totem.</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>Turns out the tuskarr aren't real choosy about...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BATTLECRY</td>
    </tr>
    <tr>
      <th>AT_047</th>
      <td>SHAMAN</td>
      <td>MINION</td>
      <td>Draenei Totemcarver</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Gain +1/+1 for each friendly...</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>It's nice to find a real craftsman in this day...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BATTLECRY</td>
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
      <th>TB_SPT_DPromoSecret3</th>
      <td>WARRIOR</td>
      <td>SPELL</td>
      <td>Visions of Valor</td>
      <td>TB</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When your opponent summons a Le...</td>
      <td>2.0</td>
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
      <td>SECRET</td>
    </tr>
    <tr>
      <th>TB_SPT_DPromoSecret4</th>
      <td>WARRIOR</td>
      <td>SPELL</td>
      <td>Visions of Fate</td>
      <td>TB</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When your opponent takes lethal...</td>
      <td>2.0</td>
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
      <td>SECRET</td>
    </tr>
    <tr>
      <th>TB_SPT_DPromoSecret5</th>
      <td>WARRIOR</td>
      <td>SPELL</td>
      <td>Visions of the Amazon</td>
      <td>TB</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When your opponent summons a mi...</td>
      <td>2.0</td>
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
      <td>SECRET</td>
    </tr>
    <tr>
      <th>TB_SPT_DPromoSecret6</th>
      <td>WARRIOR</td>
      <td>SPELL</td>
      <td>Visions of the Sorcerer</td>
      <td>TB</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When your opponent summons a mi...</td>
      <td>2.0</td>
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
      <td>SECRET</td>
    </tr>
    <tr>
      <th>TB_SPT_DPromoSecret7</th>
      <td>WARRIOR</td>
      <td>SPELL</td>
      <td>Visions of the Necromancer</td>
      <td>TB</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When your opponent summons a mi...</td>
      <td>2.0</td>
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
      <td>SECRET</td>
    </tr>
    <tr>
      <th>TB_SPT_DPromoSecret9</th>
      <td>WARRIOR</td>
      <td>SPELL</td>
      <td>Visions of Knowledge</td>
      <td>TB</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When your opponent's hand has 9...</td>
      <td>2.0</td>
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
      <td>SECRET</td>
    </tr>
    <tr>
      <th>TB_SPT_DPromo_Hero2</th>
      <td>WARRIOR</td>
      <td>HERO</td>
      <td>The Cow King</td>
      <td>TB</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>30.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>InvisibleDeathrattle</td>
    </tr>
    <tr>
      <th>TB_SPT_DpromoPortal</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Enigmatic Portal</td>
      <td>TB</td>
      <td>At the start of next turn, your hero is transf...</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>10.0</td>
      <td>NaN</td>
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
      <th>TB_SPT_DpromoPortal</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Enigmatic Portal</td>
      <td>TB</td>
      <td>At the start of next turn, your hero is transf...</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>10.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>IMMUNE</td>
    </tr>
    <tr>
      <th>TB_SPT_Minion1</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Shieldsman</td>
      <td>TB</td>
      <td>&lt;b&gt;Taunt&lt;/b&gt;\n&lt;b&gt;Battlecry:&lt;/b&gt; Gain Health eq...</td>
      <td>2.0</td>
      <td>0.0</td>
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
      <td>TAUNT</td>
    </tr>
    <tr>
      <th>TB_SPT_Minion2</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Battle Standard</td>
      <td>TB</td>
      <td>Adjacent minions have +2 Attack.</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>ADJACENT_BUFF</td>
    </tr>
    <tr>
      <th>TB_SPT_Minion2</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Battle Standard</td>
      <td>TB</td>
      <td>Adjacent minions have +2 Attack.</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>AURA</td>
    </tr>
    <tr>
      <th>TU4c_003</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Barrel</td>
      <td>MISSIONS</td>
      <td>Is something in this barrel?</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>COMMON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DEATHRATTLE</td>
    </tr>
    <tr>
      <th>TU4c_008e</th>
      <td>NEUTRAL</td>
      <td>ENCHANTMENT</td>
      <td>Might of Mukla</td>
      <td>MISSIONS</td>
      <td>King Mukla has +8 Attack this turn.</td>
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
      <td>NaN</td>
      <td>TAG_ONE_TURN_EFFECT</td>
    </tr>
    <tr>
      <th>TU4f_007</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Crazy Monkey</td>
      <td>MISSIONS</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Throw Bananas.</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>COMMON</td>
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
      <th>XXX_001</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Damage 1</td>
      <td>CHEAT</td>
      <td>Deal $1 damage.</td>
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
      <th>XXX_002</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Damage 5</td>
      <td>CHEAT</td>
      <td>Deal $5 damage.</td>
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
      <th>XXX_008</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Freeze</td>
      <td>CHEAT</td>
      <td>&lt;b&gt;Freeze&lt;/b&gt; a character.</td>
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
      <td>FREEZE</td>
    </tr>
    <tr>
      <th>XXX_020</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Damage all but 1</td>
      <td>CHEAT</td>
      <td>Set the Health of a character to 1.</td>
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
      <th>XXX_060</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Damage All</td>
      <td>CHEAT</td>
      <td>Set the Health of a character to 0.</td>
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
      <td>ImmuneToSpellpower</td>
    </tr>
    <tr>
      <th>XXX_100</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Yogg-Saron Test (Manual)</td>
      <td>CHEAT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Cast each spell you've cast ...</td>
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
      <th>XXX_101</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Set health to full</td>
      <td>CHEAT</td>
      <td>Set a character's health to full, and removes ...</td>
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
      <th>XXX_102</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Add 1 to Health.</td>
      <td>CHEAT</td>
      <td>Adds 1 health to a damaged character. Does NOT...</td>
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
      <th>XXX_103</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Add 2 to Health</td>
      <td>CHEAT</td>
      <td>Adds 2 health to a damaged character. Does NOT...</td>
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
      <th>XXX_104</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Add 4 to Health.</td>
      <td>CHEAT</td>
      <td>Adds 4 health to a damaged character. Does NOT...</td>
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


```python
# First performed an inner join, which only includes records that are present in both tables.  
# Although there were 2819 records in the left table, there were only 1079 records that existed in both tables, 
# which are what you see in the resulting dataframe. 
```

## Other Types of Joins

By default, the `.join()` method performs a left join if no parameter is passed in for `how=`.  In the cell below, perform a **_Left Join_** of `cards_with_mechanics_df` and `play_requirements_df`, with `cards_with_mechanics_df` as the left table.  

Then, display `left_join_df` to inspect our results. 


```python
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
      <th>AT_010</th>
      <td>HUNTER</td>
      <td>MINION</td>
      <td>Ram Wrangler</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; If you have a Beast, summon ...</td>
      <td>5.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>Not getting trampled is really the trick here.</td>
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
      <th>AT_011e</th>
      <td>NEUTRAL</td>
      <td>ENCHANTMENT</td>
      <td>Light's Blessing</td>
      <td>TGT</td>
      <td>Increased Attack.</td>
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
      <td>NaN</td>
      <td>AURA</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>AT_012</th>
      <td>PRIEST</td>
      <td>MINION</td>
      <td>Spawn of Shadows</td>
      <td>TGT</td>
      <td>&lt;b&gt;Inspire:&lt;/b&gt; Deal 4 damage to each hero.</td>
      <td>4.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>What did you expect to happen?  He's a Spawn. ...</td>
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
      <th>AT_017</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Twilight Guardian</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; If you're holding a Dragon, ...</td>
      <td>4.0</td>
      <td>2.0</td>
      <td>6.0</td>
      <td>EPIC</td>
      <td>1.0</td>
      <td>A result of magical experiments carried out by...</td>
      <td>DRAGON</td>
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
      <th>AT_018</th>
      <td>PRIEST</td>
      <td>MINION</td>
      <td>Confessor Paletress</td>
      <td>TGT</td>
      <td>&lt;b&gt;Inspire:&lt;/b&gt; Summon a random &lt;b&gt;Legendary&lt;/...</td>
      <td>7.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>LEGENDARY</td>
      <td>1.0</td>
      <td>She sees into your past and makes you face you...</td>
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
      <th>AT_019</th>
      <td>WARLOCK</td>
      <td>MINION</td>
      <td>Dreadsteed</td>
      <td>TGT</td>
      <td>&lt;b&gt;Deathrattle:&lt;/b&gt; Summon a Dreadsteed.</td>
      <td>4.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>EPIC</td>
      <td>1.0</td>
      <td>Crescendo himself summoned this steed, riding ...</td>
      <td>DEMON</td>
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
      <th>AT_022</th>
      <td>WARLOCK</td>
      <td>SPELL</td>
      <td>Fist of Jaraxxus</td>
      <td>TGT</td>
      <td>When you play or discard this, deal $4 damage ...</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>* Not actually Jaraxxus' fist.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>InvisibleDeathrattle</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>AT_023</th>
      <td>WARLOCK</td>
      <td>MINION</td>
      <td>Void Crusher</td>
      <td>TGT</td>
      <td>&lt;b&gt;Inspire:&lt;/b&gt; Destroy a random minion for ea...</td>
      <td>6.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>We like to call him "Wesley".</td>
      <td>DEMON</td>
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
      <th>AT_028</th>
      <td>ROGUE</td>
      <td>MINION</td>
      <td>Shado-Pan Rider</td>
      <td>TGT</td>
      <td>&lt;b&gt;Combo:&lt;/b&gt; Gain +3 Attack.</td>
      <td>5.0</td>
      <td>3.0</td>
      <td>7.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>He needed a break after that business in the V...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>COMBO</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>AT_030</th>
      <td>ROGUE</td>
      <td>MINION</td>
      <td>Undercity Valiant</td>
      <td>TGT</td>
      <td>&lt;b&gt;Combo:&lt;/b&gt; Deal 1 damage.</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>Almost went to play for Stormwind before signi...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Deal 1 damage.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>COMBO</td>
      <td>REQ_TARGET_FOR_COMBO</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>AT_032</th>
      <td>ROGUE</td>
      <td>MINION</td>
      <td>Shady Dealer</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; If you have a Pirate, gain +...</td>
      <td>3.0</td>
      <td>4.0</td>
      <td>3.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>I have great deal for you... for 4 damage to y...</td>
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
      <th>AT_035t</th>
      <td>ROGUE</td>
      <td>SPELL</td>
      <td>Ambush!</td>
      <td>TGT</td>
      <td>When you draw this, summon a 4/4 Nerubian for ...</td>
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
      <td>TOPDECK</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>AT_036</th>
      <td>ROGUE</td>
      <td>MINION</td>
      <td>Anub'arak</td>
      <td>TGT</td>
      <td>&lt;b&gt;Deathrattle:&lt;/b&gt; Return this to your hand a...</td>
      <td>9.0</td>
      <td>8.0</td>
      <td>4.0</td>
      <td>LEGENDARY</td>
      <td>1.0</td>
      <td>Was actually a pretty nice guy before, you kno...</td>
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
      <th>AT_037</th>
      <td>DRUID</td>
      <td>SPELL</td>
      <td>Living Roots</td>
      <td>TGT</td>
      <td>&lt;b&gt;Choose One -&lt;/b&gt; Deal $2 damage; or Summon ...</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>2 out of 2 saplings recommend that you summon ...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CHOOSE_ONE</td>
      <td>REQ_TARGET_TO_PLAY</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>AT_038</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Darnassus Aspirant</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Gain an empty Mana Crystal.\...</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>She loves mana crystals, she hates mana crysta...</td>
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
      <th>AT_038</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Darnassus Aspirant</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Gain an empty Mana Crystal.\...</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>She loves mana crystals, she hates mana crysta...</td>
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
      <th>AT_039</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Savage Combatant</td>
      <td>TGT</td>
      <td>&lt;b&gt;Inspire:&lt;/b&gt; Give your hero\n+2 Attack this...</td>
      <td>4.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>Maybe if you whistle a tune it will soothe him...</td>
      <td>BEAST</td>
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
      <th>AT_039e</th>
      <td>DRUID</td>
      <td>ENCHANTMENT</td>
      <td>Savage</td>
      <td>TGT</td>
      <td>+2 Attack this turn.</td>
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
      <td>NaN</td>
      <td>TAG_ONE_TURN_EFFECT</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>AT_040</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Wildwalker</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Give a friendly Beast +3 Hea...</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>She was born to be something.  She is just not...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BATTLECRY</td>
      <td>REQ_FRIENDLY_TARGET</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>AT_040</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Wildwalker</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Give a friendly Beast +3 Hea...</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>She was born to be something.  She is just not...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BATTLECRY</td>
      <td>REQ_TARGET_IF_AVAILABLE</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>AT_040</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Wildwalker</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Give a friendly Beast +3 Hea...</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>She was born to be something.  She is just not...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BATTLECRY</td>
      <td>REQ_TARGET_WITH_RACE</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>AT_040</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Wildwalker</td>
      <td>TGT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Give a friendly Beast +3 Hea...</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>4.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>She was born to be something.  She is just not...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BATTLECRY</td>
      <td>REQ_MINION_TARGET</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>AT_042</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Druid of the Saber</td>
      <td>TGT</td>
      <td>&lt;b&gt;Choose One -&lt;/b&gt; Transform to gain &lt;b&gt;Charg...</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>That's saberTEETH, not like curved pirate blad...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CHOOSE_ONE</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>AT_042t</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Sabertooth Lion</td>
      <td>TGT</td>
      <td>&lt;b&gt;Charge&lt;/b&gt;</td>
      <td>2.0</td>
      <td>2.0</td>
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
      <td>CHARGE</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>AT_042t2</th>
      <td>DRUID</td>
      <td>MINION</td>
      <td>Sabertooth Panther</td>
      <td>TGT</td>
      <td>&lt;b&gt;Stealth&lt;/b&gt;</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>COMMON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>BEAST</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>STEALTH</td>
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
      <th>TB_SPT_DPromoSecret3</th>
      <td>WARRIOR</td>
      <td>SPELL</td>
      <td>Visions of Valor</td>
      <td>TB</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When your opponent summons a Le...</td>
      <td>2.0</td>
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
      <td>SECRET</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>TB_SPT_DPromoSecret4</th>
      <td>WARRIOR</td>
      <td>SPELL</td>
      <td>Visions of Fate</td>
      <td>TB</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When your opponent takes lethal...</td>
      <td>2.0</td>
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
      <td>SECRET</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>TB_SPT_DPromoSecret5</th>
      <td>WARRIOR</td>
      <td>SPELL</td>
      <td>Visions of the Amazon</td>
      <td>TB</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When your opponent summons a mi...</td>
      <td>2.0</td>
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
      <td>SECRET</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>TB_SPT_DPromoSecret6</th>
      <td>WARRIOR</td>
      <td>SPELL</td>
      <td>Visions of the Sorcerer</td>
      <td>TB</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When your opponent summons a mi...</td>
      <td>2.0</td>
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
      <td>SECRET</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>TB_SPT_DPromoSecret7</th>
      <td>WARRIOR</td>
      <td>SPELL</td>
      <td>Visions of the Necromancer</td>
      <td>TB</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When your opponent summons a mi...</td>
      <td>2.0</td>
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
      <td>SECRET</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>TB_SPT_DPromoSecret9</th>
      <td>WARRIOR</td>
      <td>SPELL</td>
      <td>Visions of Knowledge</td>
      <td>TB</td>
      <td>&lt;b&gt;Secret:&lt;/b&gt; When your opponent's hand has 9...</td>
      <td>2.0</td>
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
      <td>SECRET</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>TB_SPT_DPromo_Hero2</th>
      <td>WARRIOR</td>
      <td>HERO</td>
      <td>The Cow King</td>
      <td>TB</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>30.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>InvisibleDeathrattle</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>TB_SPT_DpromoPortal</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Enigmatic Portal</td>
      <td>TB</td>
      <td>At the start of next turn, your hero is transf...</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>10.0</td>
      <td>NaN</td>
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
      <th>TB_SPT_DpromoPortal</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Enigmatic Portal</td>
      <td>TB</td>
      <td>At the start of next turn, your hero is transf...</td>
      <td>4.0</td>
      <td>0.0</td>
      <td>10.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>IMMUNE</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>TB_SPT_Minion1</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Shieldsman</td>
      <td>TB</td>
      <td>&lt;b&gt;Taunt&lt;/b&gt;\n&lt;b&gt;Battlecry:&lt;/b&gt; Gain Health eq...</td>
      <td>2.0</td>
      <td>0.0</td>
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
      <td>TAUNT</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>TB_SPT_Minion2</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Battle Standard</td>
      <td>TB</td>
      <td>Adjacent minions have +2 Attack.</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>ADJACENT_BUFF</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>TB_SPT_Minion2</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Battle Standard</td>
      <td>TB</td>
      <td>Adjacent minions have +2 Attack.</td>
      <td>2.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>AURA</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>TU4c_003</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Barrel</td>
      <td>MISSIONS</td>
      <td>Is something in this barrel?</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2.0</td>
      <td>COMMON</td>
      <td>NaN</td>
      <td>NaN</td>
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
      <th>TU4c_008e</th>
      <td>NEUTRAL</td>
      <td>ENCHANTMENT</td>
      <td>Might of Mukla</td>
      <td>MISSIONS</td>
      <td>King Mukla has +8 Attack this turn.</td>
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
      <td>NaN</td>
      <td>TAG_ONE_TURN_EFFECT</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>TU4f_007</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Crazy Monkey</td>
      <td>MISSIONS</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Throw Bananas.</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>COMMON</td>
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
      <th>XXX_001</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Damage 1</td>
      <td>CHEAT</td>
      <td>Deal $1 damage.</td>
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
      <th>XXX_002</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Damage 5</td>
      <td>CHEAT</td>
      <td>Deal $5 damage.</td>
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
      <th>XXX_008</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Freeze</td>
      <td>CHEAT</td>
      <td>&lt;b&gt;Freeze&lt;/b&gt; a character.</td>
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
      <td>FREEZE</td>
      <td>REQ_TARGET_TO_PLAY</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>XXX_020</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Damage all but 1</td>
      <td>CHEAT</td>
      <td>Set the Health of a character to 1.</td>
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
      <th>XXX_060</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Damage All</td>
      <td>CHEAT</td>
      <td>Set the Health of a character to 0.</td>
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
      <td>ImmuneToSpellpower</td>
      <td>REQ_TARGET_TO_PLAY</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>XXX_100</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Yogg-Saron Test (Manual)</td>
      <td>CHEAT</td>
      <td>&lt;b&gt;Battlecry:&lt;/b&gt; Cast each spell you've cast ...</td>
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
      <th>XXX_101</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Set health to full</td>
      <td>CHEAT</td>
      <td>Set a character's health to full, and removes ...</td>
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
      <th>XXX_102</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Add 1 to Health.</td>
      <td>CHEAT</td>
      <td>Adds 1 health to a damaged character. Does NOT...</td>
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
      <th>XXX_103</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Add 2 to Health</td>
      <td>CHEAT</td>
      <td>Adds 2 health to a damaged character. Does NOT...</td>
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
      <th>XXX_104</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Add 4 to Health.</td>
      <td>CHEAT</td>
      <td>Adds 4 health to a damaged character. Does NOT...</td>
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


```python
# Every record from cards_with_mechanics_df, as well as any records from play_requirements_df that have matching index values 
# with a record from the left table.  
```

#### Outer Joins

In the cell below, perform an outer join between `cards_df` and `dust_df`. Since these tables contain columns with the same name, we'll need to specify a suffix for at least one of them, so that the column can be renamed to avoid a naming collision. 

During this join, set the `rsuffix` parameter to `_dust`


```python
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
      <td>CRAFTING_GOLDEN</td>
      <td>800.0</td>
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
      <td>DISENCHANT_NORMAL</td>
      <td>20.0</td>
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
      <td>DISENCHANT_GOLDEN</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>AT_003</th>
      <td>MAGE</td>
      <td>MINION</td>
      <td>Fallen Hero</td>
      <td>TGT</td>
      <td>Your Hero Power deals 1 extra damage.</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>And he can't get up.</td>
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
      <th>AT_003</th>
      <td>MAGE</td>
      <td>MINION</td>
      <td>Fallen Hero</td>
      <td>TGT</td>
      <td>Your Hero Power deals 1 extra damage.</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>And he can't get up.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CRAFTING_GOLDEN</td>
      <td>800.0</td>
    </tr>
    <tr>
      <th>AT_003</th>
      <td>MAGE</td>
      <td>MINION</td>
      <td>Fallen Hero</td>
      <td>TGT</td>
      <td>Your Hero Power deals 1 extra damage.</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>And he can't get up.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DISENCHANT_NORMAL</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>AT_003</th>
      <td>MAGE</td>
      <td>MINION</td>
      <td>Fallen Hero</td>
      <td>TGT</td>
      <td>Your Hero Power deals 1 extra damage.</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>And he can't get up.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DISENCHANT_GOLDEN</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>AT_004</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Arcane Blast</td>
      <td>TGT</td>
      <td>Deal $2 damage to a minion. This spell gets do...</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>EPIC</td>
      <td>1.0</td>
      <td>Now with 100% more blast!</td>
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
      <th>AT_004</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Arcane Blast</td>
      <td>TGT</td>
      <td>Deal $2 damage to a minion. This spell gets do...</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>EPIC</td>
      <td>1.0</td>
      <td>Now with 100% more blast!</td>
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
      <th>AT_004</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Arcane Blast</td>
      <td>TGT</td>
      <td>Deal $2 damage to a minion. This spell gets do...</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>EPIC</td>
      <td>1.0</td>
      <td>Now with 100% more blast!</td>
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
      <th>AT_004</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Arcane Blast</td>
      <td>TGT</td>
      <td>Deal $2 damage to a minion. This spell gets do...</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>EPIC</td>
      <td>1.0</td>
      <td>Now with 100% more blast!</td>
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
      <th>AT_005</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Polymorph: Boar</td>
      <td>TGT</td>
      <td>Transform a minion into a 4/2 Boar with &lt;b&gt;Cha...</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>It's always Huffer.</td>
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
      <th>AT_005</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Polymorph: Boar</td>
      <td>TGT</td>
      <td>Transform a minion into a 4/2 Boar with &lt;b&gt;Cha...</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>It's always Huffer.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CRAFTING_GOLDEN</td>
      <td>800.0</td>
    </tr>
    <tr>
      <th>AT_005</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Polymorph: Boar</td>
      <td>TGT</td>
      <td>Transform a minion into a 4/2 Boar with &lt;b&gt;Cha...</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>It's always Huffer.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DISENCHANT_NORMAL</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>AT_005</th>
      <td>MAGE</td>
      <td>SPELL</td>
      <td>Polymorph: Boar</td>
      <td>TGT</td>
      <td>Transform a minion into a 4/2 Boar with &lt;b&gt;Cha...</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>RARE</td>
      <td>1.0</td>
      <td>It's always Huffer.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DISENCHANT_GOLDEN</td>
      <td>100.0</td>
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
      <td>CRAFTING_NORMAL</td>
      <td>40.0</td>
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
      <td>CRAFTING_GOLDEN</td>
      <td>400.0</td>
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
      <td>DISENCHANT_NORMAL</td>
      <td>5.0</td>
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
      <td>DISENCHANT_GOLDEN</td>
      <td>50.0</td>
    </tr>
    <tr>
      <th>AT_006e</th>
      <td>MAGE</td>
      <td>ENCHANTMENT</td>
      <td>Power of Dalaran</td>
      <td>TGT</td>
      <td>Increased Spell Damage.</td>
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
      <td>NaN</td>
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
      <td>CRAFTING_NORMAL</td>
      <td>40.0</td>
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
      <td>CRAFTING_GOLDEN</td>
      <td>400.0</td>
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
      <td>DISENCHANT_NORMAL</td>
      <td>5.0</td>
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
      <td>DISENCHANT_GOLDEN</td>
      <td>50.0</td>
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
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>XXX_111</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>AI Buddy - All Charge, All Windfury!</td>
      <td>CHEAT</td>
      <td>Play this card to give all minions &lt;b&gt;Charge&lt;/...</td>
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
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>XXX_111e</th>
      <td>NEUTRAL</td>
      <td>ENCHANTMENT</td>
      <td>All Charge, All Windfury, All The Time</td>
      <td>CHEAT</td>
      <td>Your minions always have &lt;b&gt;Charge&lt;/b&gt; and &lt;b&gt;...</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>XXX_112</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Fill Deck</td>
      <td>CHEAT</td>
      <td>Fill target hero's deck with random cards.</td>
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
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>XXX_113</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Again</td>
      <td>CHEAT</td>
      <td>NaN</td>
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
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>XXX_115</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Destroy Played Cards</td>
      <td>CHEAT</td>
      <td>Whenever a player summons a minion, destroy it.</td>
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
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>XXX_115e</th>
      <td>NEUTRAL</td>
      <td>ENCHANTMENT</td>
      <td>Destroy Played Card Enchantment</td>
      <td>CHEAT</td>
      <td>Whenever a player summons a minion, destroy it.</td>
      <td>NaN</td>
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
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>XXX_119</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Death No Rattle</td>
      <td>CHEAT</td>
      <td>Died without triggering &lt;b&gt;Deathrattle&lt;/b&gt;, Al...</td>
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
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>XXX_119e</th>
      <td>NaN</td>
      <td>ENCHANTMENT</td>
      <td>Death No Rattle</td>
      <td>CHEAT</td>
      <td>Died without triggering &lt;b&gt;Deathrattle&lt;/b&gt;, Al...</td>
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
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>XXX_999_Crash</th>
      <td>NEUTRAL</td>
      <td>SPELL</td>
      <td>Crash the server</td>
      <td>CHEAT</td>
      <td>Crash the server</td>
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
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>ds1_whelptoken</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Whelp</td>
      <td>EXPERT1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DRAGON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
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
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>skele11</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Skeleton</td>
      <td>CORE</td>
      <td>&lt;b&gt;&lt;/b&gt;</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>COMMON</td>
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
      <th>skele21</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Damaged Golem</td>
      <td>EXPERT1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>COMMON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>MECHANICAL</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CRAFTING_NORMAL</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>skele21</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Damaged Golem</td>
      <td>EXPERT1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>COMMON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>MECHANICAL</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>CRAFTING_GOLDEN</td>
      <td>400.0</td>
    </tr>
    <tr>
      <th>skele21</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Damaged Golem</td>
      <td>EXPERT1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>COMMON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>MECHANICAL</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DISENCHANT_NORMAL</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>skele21</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Damaged Golem</td>
      <td>EXPERT1</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>1.0</td>
      <td>COMMON</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>MECHANICAL</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>DISENCHANT_GOLDEN</td>
      <td>50.0</td>
    </tr>
    <tr>
      <th>tt_004</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Flesheating Ghoul</td>
      <td>EXPERT1</td>
      <td>Whenever a minion dies, gain +1 Attack.</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>'Flesheating' is an unfair name.  It's just th...</td>
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
      <th>tt_004</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Flesheating Ghoul</td>
      <td>EXPERT1</td>
      <td>Whenever a minion dies, gain +1 Attack.</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>'Flesheating' is an unfair name.  It's just th...</td>
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
      <th>tt_004</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Flesheating Ghoul</td>
      <td>EXPERT1</td>
      <td>Whenever a minion dies, gain +1 Attack.</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>'Flesheating' is an unfair name.  It's just th...</td>
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
      <th>tt_004</th>
      <td>NEUTRAL</td>
      <td>MINION</td>
      <td>Flesheating Ghoul</td>
      <td>EXPERT1</td>
      <td>Whenever a minion dies, gain +1 Attack.</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>COMMON</td>
      <td>1.0</td>
      <td>'Flesheating' is an unfair name.  It's just th...</td>
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
      <th>tt_004o</th>
      <td>NEUTRAL</td>
      <td>ENCHANTMENT</td>
      <td>Cannibalize</td>
      <td>EXPERT1</td>
      <td>Increased Attack.</td>
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
      <td>NaN</td>
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
      <td>CRAFTING_NORMAL</td>
      <td>400.0</td>
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
      <td>CRAFTING_GOLDEN</td>
      <td>1600.0</td>
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
      <td>DISENCHANT_NORMAL</td>
      <td>100.0</td>
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
