# Sunrise and sunset times

## sunrise.m
This function computes sunrise and sunset times from any location on Earth (latitude, longitude and altitude), for a given date and timezone, and also computes the reverse problem: latitude/longitude from sunrise/sunset times. Without any input argument, `sunrise` will try to guess your location (needs an internet connection) and give you the local sunset and sunrise times. There is also two original reverse functions:
- with option `'day2lat'`: computes the latitude from the day length;
- with option `'sun2ll'`: computes the latitude and longitude from sunrise and sunset date/time.
Both reverse functions need the altitude as an input argument.

The function is fully vectorized so any input parameters can be scalars, vectors or matrix (of the same size). This allows to compute in a single command, for example, the 365 different day lengths at a single location, or even for a full grid of latitudes and longitudes using a 3D matrix:

![](sunrise.gif)

Examples:

To get sunrise/sunset of your current location:
```matlab
>> sunrise
Location: 48.8582 °N, 2.3387 °E, 0 m
Sunrise: 10-Oct-2017 08:03:41 +02
Sunset: 10-Oct-2017 19:13:49 +02
Day length: 11h 10mn 8s
```

To compute the latitude corresponding to 14 hours of daylight at altitude 0m on the 21 April 2019:
```matlab
>> sunrise(14/24,0,'2019-04-21','day2lat')
Estimated latitude: 49.076°N
```

To compute the latitude and longitude corresponding to specific sunrise and sunset times:
```matlab
>> sunrise('22-Apr-2019 04:52:12','22-Apr-2019 18:51:04',0,'sun2ll')
Estimated location: 47.9995°N, 2.00142°E
```

![](sunrise_example.png)


## Author
**François Beauducel**, [IPGP](www.ipgp.fr), [beaudu](https://github.com/beaudu), beauducel@ipgp.fr

## Documentation
Type `help sunrise` or `doc sunrise` to get syntax and full documentation. See the function code for further explanations, and [![View SUNRISE: sunrise and sunset times on File Exchange](https://www.mathworks.com/matlabcentral/images/matlab-file-exchange.svg)](https://fr.mathworks.com/matlabcentral/fileexchange/64692-sunrise-sunrise-and-sunset-times) for users community comments.
