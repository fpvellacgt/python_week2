# python_week2

import pandas as pd 

####reading in data 
en = pd.read_csv("data/orig/encounters.csv")
# en.info()
ev = pd.read_csv("data/orig/evolutions.csv")
lo = pd.read_csv("data/orig/locations.csv")
mo = pd.read_csv("data/orig/moves.csv")
pm = pd.read_csv("data/orig/poke_moves.csv")
pk = pd.read_csv("data/orig/pokemon.csv")
re = pd.read_csv("data/orig/regions.csv")

###### cleaning data
en.isnull().sum().sum() ##0
en.to_csv("data/clean/encounters.csv")

ev.isnull().sum().sum() ##6414  
####see how many blanks 
missing = ev.columns[ev.isnull().any()]
print(missing) #### telling you what columns are missing data
##### this does not have to be done
ev.fillna(10,inplace=True) 
#### fill the NANs with the number 10 
ev.to_csv("data/clean/evolutions.csv")
### moves to the CLEAN DATA FOLDER


lo.isnull().sum().sum() ##91
lo.fillna("special events",inplace=True)
lo.to_csv("data/clean/locations.csv")

mo.isnull().sum().sum() ##2499
missing = mo.columns[mo.isnull().any()]
print(missing)
mo.fillna(10,inplace=True)
mo.to_csv("data/clean/moves.csv")

pm.isnull().sum().sum() ##494679
missing = pm.columns[pm.isnull().any()]
print(missing)
pm.fillna(10,inplace=True)
pm.to_csv("data/clean/poke_moves.csv")

pk.isnull().sum().sum() ##0
pk.to_csv("data/clean/pokemon.csv")

re.isnull().sum().sum() ##0
re.to_csv("data/clean/regions.csv")

####### Reading in clean data

en = pd.read_csv("data/clean/encounters.csv")
ev = pd.read_csv("data/clean/evolutions.csv")
lo = pd.read_csv("data/clean/locations.csv")
mo = pd.read_csv("data/clean/moves.csv")
pm = pd.read_csv("data/clean/poke_moves.csv")
pk = pd.read_csv("data/clean/pokemon.csv")
re = pd.read_csv("data/clean/regions.csv")

#### Starting 
pm.info()
pk.info()

pmk = pk.merge(pm, how="left", left_on="id", right_on="pokemon_id", suffixes=('_poke', "_moves"))
## creating a merge variable name called PMK
### has the datasets of pk and pm for the poke_moves and pokemon dataset
#### left_on has to have the same name in both datasets to merge  --- first column name
#### right_on is telling you where in the lineup to move the dataset together
######## suffixes are adding the names _poke and _moves to the orginal dataset of where the come from to know what you are lokking at 
#### these are just for over lap of names in both datasets
pmk.info()

pmk[['identifier_poke', 'identifier_moves']].head().drop_duplicates()

#### With this code, you can use funtions to view certain lists. 
#### Such as , search by name and by region. 
