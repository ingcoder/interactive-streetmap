# interactive-streetmap
Interactive streetmap showing traffic lights in downtown San Diego


### Import libraries
    !pip install geopandas descartes shapely rtree
    import geopandas
    import descartes
    import matplotlib.pyplot as plt
    import pandas as pd
    from shapely.geometry import Point, Polygon
    import folium
    
### Load and show traffic data from csv file
    station_lights =  pd.read_csv('traffic_lights_data_2015.csv') 
    station_lights.head()
    
    locationlist = station_lights[['lights_lat', 'lights_long']].values.tolist()
    print(locationlist)

    street_lights =  pd.read_csv('StreetLight_LocationsClean.csv')
    street_lights.shape
    

