from urllib.request import urlopen
import json
import time
import csv

###########################
# @Ned Hulseman          #
# @10/02/2017            #
##########################

#This script interacts with Weather Undergrounds API
#To pull forecast data and writes the data to a csv


#This is a list of locations that the script will pull from, these 
#can easily be changed.
locations = [\
  'AR/Buenos-Aires.json',\
  'SJK.json',\
  'CA/Nanaimo.json',\
  'zmw:00000.287.78764.json',\
  'CN/Ningbo.json',\
  'EG/Cairo.json',\
  'EDFM.json',\
  'IN/Mumbai.json',\
  'OIIE.json',\
  'KG/Bishkek.json',\
  'LV/Riga.json',\
  'PK/Quetta.json',\
  'MNL.json',\
  'PL/Warsaw.json',\
  'SA/Dhahran.json',\
  'ES/Madrid.json',\
  'GB/Oldham.json',\
  'AK/Anchorage.json'\
]

#Creates a header to output to a csv
heading=['city', 'min_1', 'max_1', 'min_2', 'max_2', 'min_3', 'max_3', 'min_4', 'max_4', 'min_5', 'max_5']

#Prepares csv and writes the header to the csv
out=open('temp.csv', 'w', newline='')
writer=csv.writer(out)
writer.writerow(heading)

#outter for-loop iterates through the list of locations
for i in range(len(locations)):
    #creates a url string and concatenates the given location to it 
    link_string = 'http://api.wunderground.com/api/dc44b88239b5bb92/forecast10day/conditions/q/%s'%(locations[i])
    path=urlopen(link_string)
    json_string=path.read().decode("utf-8") #imports entire json for a location, but we are only interested in the forecasts
    parsed_json = json.loads(json_string)
    
    #navigates through the json dictionary listings 
    country=parsed_json['current_observation']['display_location']['full']
    print(country)
     
    #reads in 5 day forecast for high and low and saves to 10 respective variables
    forecastday=parsed_json['forecast']['simpleforecast']['forecastday']
    for day in forecastday:
        for j in range(1, 6):
            if day['period']==(j):
                if j==1:
                    day1_high=day['high']['celsius']
                    day1_low=day['low']['celsius']
                elif j==2:
                    day2_high=day['high']['celsius']
                    day2_low=day['low']['celsius']
                elif j==3:
                    day3_high=day['high']['celsius']
                    day3_low=day['low']['celsius']
                elif j==4:
                    day4_high=day['high']['celsius']
                    day4_low=day['low']['celsius']
                elif j==5:
                    day5_high=day['high']['celsius']
                    day5_low=day['low']['celsius']
    #writes the entire row for the given country            
    writer.writerow([country, day1_low, day1_high, day2_low, day2_high, day3_low, day3_high, day4_low, day4_high, day5_low, day5_high])
    path.close()
    time.sleep(6) #sleeps through each iteration of the outter for loop in compliance with WU scraping policies
    

out.close()
print('Done!')
