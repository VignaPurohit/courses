# Creating Spatial Data

A common operation in spatial analysis is to take non-spatial data, such as CSV files, and creating a spatial dataset from it using coordinate information contained in the file. GeoPandas provides a convenient way to take data from a delimited-text file, create geometry and write the results as a spatial dataset.

We will read a tab-delimited file of places, filter it to a feature class, create a GeoDataFrame and export it as a GeoPackage file.

![](images/python_foundation/geonames_mountains.png)


```python
import os
import pandas as pd
import geopandas as gpd
```


```python
data_pkg_path = 'data/geonames/'
filename = 'US.txt'
path = os.path.join(data_pkg_path, filename)
```

## Reading Tab-Delimited Files

The source data comes from [GeoNames](https://en.wikipedia.org/wiki/GeoNames) - a free and open database of geographic names of the world. It is a huge database containing millions of records per country. The data is distributed as country-level text files in a tab-delimited format. The files do not contain a header row with column names, so we need to specify them when reading the data. The data format is described in detail on the [Data Export](https://www.geonames.org/export/) page.

We specify the separator as **\\t** (tab) as an argument to the `read_csv()` method. Note that the file for USA has more than 2M records.


```python
column_names = [
    'geonameid', 'name', 'asciiname', 'alternatenames', 
    'latitude', 'longitude', 'feature class', 'feature code',
    'country code', 'cc2', 'admin1 code', 'admin2 code',
    'admin3 code', 'admin4 code', 'population', 'elevation',
    'dem', 'timezone', 'modification date'
]

df = pd.read_csv(path, sep='\t', names=column_names)
print(df.info())
```

## Filtering Data

The input data as a column `feature_class` categorizing the place into [9 feature classes](https://www.geonames.org/export/codes.html). We can select all rows with the value `T` with the category  *mountain,hill,rock...*


```python
mountains = df[df['feature class']=='T']
print(mountains.head()[['name', 'latitude', 'longitude', 'dem','feature class']])
```

## Creating Geometries

GeoPandas has a conveinent function `points_from_xy()` that creates a Geometry column from X and Y coordinates. We can then take a Pandas dataframe and create a GeoDataFrame by specifying a CRS and the geometry column.


```python
geometry = gpd.points_from_xy(mountains.longitude, mountains.latitude)
gdf = gpd.GeoDataFrame(mountains, crs='EPSG:4326', geometry=geometry)
print(gdf.info())
```

## Writing Files

We can write the resulting GeoDataFrame to any of the supported vector data format. Here we are writing it as a new GeoPackage file.

You can open the resulting geopackage in a GIS and view the data.


```python
output_dir = 'output'
output_filename = 'mountains.gpkg'
output_path = os.path.join(output_dir, output_filename)

gdf.to_file(driver='GPKG', filename=output_path, encoding='utf-8')
print('Successfully written output file at {}'.format(output_path))
```

## Exercise

The data package contains multiple geonames text files from different countries in the `geonames/` folder. Write code to read all the files, merge them and extract the mountain features to a single geopackage.

- Hint1: Use the `os.listdir()` method to get all files in a directory.
- Hint2: Use the Pandas method `concat()` to merge multiple dataframes.


```python
import os
import pandas as pd
import geopandas as gpd

data_pkg_path = 'data/geonames/'
files = os.listdir(data_pkg_path)

filepaths = []
for file in files:
    filepaths.append(os.path.join(data_pkg_path, file))
print(filepaths)

# Iterate over the files, read them using pandas and create a list of dataframes. 
# You can then use pd.concat() function to merge them
```

----
