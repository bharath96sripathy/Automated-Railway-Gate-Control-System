# Automated-Railway-Gate-Control-System
The objective is to design and develop automated railway gate control system. 
In conventional gate control system, the actuation of gate i.e closing of the gate and opening of the gate was done with respect to the distance from which the train is approaching towards the gate.
Distance factor was kept constant. By conventional method the 'waiting time' of vehicle and pedestrians was uncertain. 
The time taken by the train to cross the gate was variable.
With the 'Automated Railway Gate Control System' the time factor is kept constant and distance factor is kept variable.
So , the 'waiting time' at the gate is always constant irrespective of the speed and distance of the train traveled.  
##########################################################################################################################################
This projet requires:
1.MATLAB 
2.MATLAB MOBILE APP
##########################################################################################################################################
MATLAB Code:
%sets up connection with the mobile
m = mobiledev;
%starts reading values from the sensor
m.Logging = 1;
%defines the variables inside the log
[lat, lon, t, spd] = poslog(m);
%sets up the format of the output as long(upto 15 decimal places)
format long
%position of TAMBARAM railwaystation
%lat1 = 12.925018772288563;
%lon1 = 80.118232946552388;
b = spd*18/5 ;
%when logging is 'on', inside the loop the distance between the train
%location and the location of TAMBARAM railwaystation is calculated
%distance and speed relation is established and the gate closes according
%to the algorithm
while m.Logging == 1
    %d = 2*asin(sqrt((sin((lat1-lat(1,1))/2))^2 + cos(lat1)*cos(lat(1,1))*(sin((lon1-lon(1,1))/2))^2));
    %s = d*100;
    radius=6371;
    lat1=12.925000000000000*pi/180;
    lat=lat(end);
    lon=lon(end);
    lat2=round(lat(1,1),4)*pi/180;
    lon1=80.118200000000000*pi/180;
    lon2=round(lon(1,1),4)*pi/180;
    deltaLat=lat2-lat1;
    deltaLon=lon2-lon1;
    a=sin((deltaLat)/2)^2 + cos(lat1)*cos(lat2) * sin(deltaLon/2)^2;
    c=2*atan2(sqrt(a),sqrt(1-a));
    d =radius*c; %Haversine distance
    d = d(end)
    b = b(end)
    %x=deltaLon*cos((lat1+lat2)/2);
    %y=deltaLat;
    %d2km=radius*sqrt(x*x + y*y) %Pythagoran distance
    if d <=3 && b >=60 
        disp('-----------------------------------------Gate CLOSE------------------------------------------')
    elseif d <=2.5 && b >= 50
        disp('-----------------------------------------Gate CLOSE------------------------------------------')
    elseif d <=2 && b >= 40 
        disp('-----------------------------------------Gate CLOSE------------------------------------------')
    elseif d <= 1.5 && b >= 30 
        disp('-----------------------------------------Gate CLOSE------------------------------------------')
    %elseif 0.5 <= s && 1 <= s  && a == 0
     %   disp('open')
    elseif d <= 1  && b > 0
        disp('-----------------------------------------Gate CLOSE------------------------------------------')
    else
        disp('-----------------------------------------Gate OPEN-------------------------------------------')
    end
    %end
end
%stops reading the sensor values
m.Logging = 0;

########################################################################################################################################

    

