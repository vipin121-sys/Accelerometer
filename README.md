
first runn this part in your mobile in order to ON your mobile's sensor
m = mobiledev;
m.AccelerationSensorEnabled = 1;
m.Logging = 1;

then walk and run this code

m.Logging = 0;
[a,t] = accellog(m);
plot(t,a);
legend('X', 'Y', 'Z');
xlabel('Relative time (s)');
ylabel('Acceleration (m/s^2)');
x = a(:,1);
y = a(:,2);
z = a(:,3);
mag = sqrt(sum(x.^2 + y.^2 + z.^2, 2));
plot(t,mag);
xlabel('Time (s)');
ylabel('Acceleration (m/s^2)');
magNoG = mag - mean(mag);


plot(t,magNoG);
xlabel('Time (s)');
ylabel('Acceleration (m/s^2)');
minPeakHeight = std(magNoG);

[pks,locs] = findpeaks(magNoG,'MINPEAKHEIGHT',minPeakHeight);

numSteps = numel(pks)
hold on;
plot(t(locs), pks, 'r', 'Marker', 'v', 'LineStyle', 'none');
title('Counting Steps');
xlabel('Time (s)');
ylabel('Acceleration Magnitude, No Gravity (m/s^2)');
hold off;
m.AccelerationSensorEnabled = 0;
l
clear m;
