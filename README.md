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
    
### Create interactive map
    #Create folium map
    map = folium.Map(location=[32.732428,	-117.111704], tiles='Stamen Toner', zoom_start=12, control_scale=True)
    marker_cluster = folium.MarkerCluster().add_to(map)
    
    marker = folium.CircleMarker(location=[32.692872,  -117.121745], radius=8000, 
                                 fill_color='#3186cc', fill_opacity=0.1)
    marker.add_to(map)
  
    marker2 = folium.Marker(location=[32.692872,  -117.121745], popup="Traffic station_id 119030 / long:32.692872  lat:-117.121745 / Streetlights {}".format(station_lights['no. of lights'][0]) )
    marker2.add_to(map)

    for point in range(0, 20000): 
      folium.Marker(locationlist[point], popup='Traffic lights').add_to(marker_cluster)

    map

### Save html interactive map
    # Filepath to the output
    outfp = "sd_streetlights_map.html"

    # Save the map
    map.save(outfp)

    

