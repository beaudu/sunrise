# Sunrise and sunset times

## sunrise.m
This function, Matlab/GNU Octave compatible, computes sunrise and sunset times from any location on Earth (latitude, longitude and altitude), for a given date and timezone, and optionally returns noon time and day length. Based on astronomical equations, it uses an approximate correction for the influence of atmospherical refraction (a solar elevation of -0.83°).

Without any input argument, `sunrise` will try to guess your location (needs an internet connection) and your time zone and give you the local sunset and sunrise times. The function has also the original capability to compute the reverse problem, i.e., the latitude/longitude from any sunrise/sunset times:
- with option `'day2lat'`: estimates the latitude from the day length and date;
- with option `'sun2ll'`: estimates the latitude and longitude from sunrise and sunset date/time.
Both reverse functions need the altitude as an input argument.

The function is fully vectorized so any input parameters can be scalars, vectors or matrix (of the same size). This allows to compute in a single command, for example, the 365 different day lengths at a single location (see examples), or even for a full grid of latitudes and longitudes using a 3D matrix:

![](sunrise.gif)

### Examples

To get sunrise/sunset at your current location:
```matlab
>> sunrise
Location: 48.8582 °N, 2.3387 °E, 0 m
Sunrise: 10-Oct-2017 08:03:41 +02
Sunset: 10-Oct-2017 19:13:49 +02
Day length: 11h 10mn 8s
```

To compute the sunrise/sunset at Reykjavík (Iceland) on Christmas 2020:
```matlab
>> sunrise(64.13,-21.91,0,1,'25 Dec 2020')
Sunrise: 25-Dec-2020 12:24:13 +01
Sunset:  25-Dec-2020 16:33:11 +01
Day length: 4h 8mn 57s
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

To plot the sunrise, noon and sunset times variation during the year 2020 in Montmartre, Paris (48.89N, 2.34E, 130m):
```matlab
d=datenum(2020,1,1:366)';
% -- computes DST (from last Sunday of March to last Sunday of October)
dl=ones(size(d)); % Winter time GMT+1
m=str2num(datestr(d,'mm'));
k1=find(m==3 & mod(d,7)==2,1,'last'); % index of last Sunday of March
k2=find(m==10 & mod(d,7)==2,1,'last'); % index of last Sunday of October
dl(k1:k2-1) = 2; % Daylight Saving Time GMT+2
% -- computes sunset/noon/sunrise
[srise,sset,noon]=sunrise(48.89,2.34,130,dl,d);
% -- plots the results
plot(d,mod([srise,sset,noon],1),'LineWidth',3)
datetick('x','mmm'), datetick('y','HH:MM')
ylabel('Local Time (hour)')
title('Sunrise, noon, and sunset times in Paris (France)')
```

![](sunrise_example.png)


## Author
**François Beauducel**, [IPGP](www.ipgp.fr), [beaudu](https://github.com/beaudu), beauducel@ipgp.fr

## Documentation
Type `help sunrise` or `doc sunrise` to get syntax and full documentation. See the function code for further explanations, and [![View SUNRISE: sunrise and sunset times on File Exchange](https://www.mathworks.com/matlabcentral/images/matlab-file-exchange.svg)](https://fr.mathworks.com/matlabcentral/fileexchange/64692-sunrise-sunrise-and-sunset-times) for users community comments.
