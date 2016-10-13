# Lab3
This lab is about Distance Measuring from one city to another

import csv
import math
print ('I assume that nearby cities area to be in the range of 100km');
print('Enter the name of the city');
cName = raw_input();

with open('Location.csv', 'rb') as csvfile:  # Loading geo-locaion.csv file.
    myfilereader = csv.DictReader(csvfile)
    for row in myfilereader:
     if(cName == row['city']):
         latd1=float(row['latitude']);
         long1=float(row['longitude']);
         print('Longitude',row['longitude'],'Latitude',row['latitude'])
         break;

    for row in myfilereader:
        latd2= float(row['latitude']);  # Latitude of the second city.
        long2= float(row['longitude']); #Longitude of the second city.
        dlat = latd2-latd1;  # Difference between latitudes of two cities;
        dlon = long2-long1;  # Difference between longitude of two cities.

        # The radial distance between two cities By Great Circle Formula.
        x = math.pow(math.sin((dlat/2)),2) + (math.cos(latd1) * math.cos(latd2) * math.pow(math.sin((dlon/2)),2))
        y = 2 * x*math.atan2(math.sqrt(x),math.sqrt(1-x));
        d = 6373 * y;    #By Using Great Circle Formula
        if(d < 100 and d > 80):  # Printing of Distances of nearby Cities
            print('Distance of ',cName,'with Longitude/latitude',latd1,long1,' From',row['city'],'Longitude/Latitude',latd2,long2,'is',int(d),'km');
        
