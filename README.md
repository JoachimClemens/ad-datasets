# AD Datasets

This repository contains autonomous driving datasets used in the following paper:


## Research Vehicle

The research vehicle was a Volkswagen Passat B8.
It has a wheel base of 2.786 m and a rear track width of 1.568 m.
It is equipped with an IMU, that is mounted above the center of the rear axle.
Furthermore, the velocity as well as the steering angle is reported via CAN.
Finally, a ublox F9P GNSS receiver with RTK correction is used as reference.
The corresponding antenna is mounted on the roof above the center of the rear axle.


## General Structure of Data

Each line, separated by `\n`, contains one measurement, while the fields of a measurement are separated by `,`.
The measurements have the following structure:

    <tag>,<timestamp>,<value 1>,<value 2>,...

* `<tag>`: identifier of the measurement (see below)
* `<timestamp>`: timestamp in microseconds
* `<value 1>,<value 2>,...`: values of the measurement (see below)

## Measurements

The measurements are identified by the tag.
They are described below.

### IMU Measurement 

Acceleration and turn rate measured by the IMU.

Tag: `IMU`

Structure: `IMU,<timestamp>,<acc x>,<acc y>,<acc z>,<gyr x>,<gyr y>,<gyr z>`

Example: `IMU,911640478,0.6754188929602051,0.4865515767382812,9.212656828110962,0.00729390820408646,-0.001332533956709867,0.05594985599351197`

Fields:

1. `<acc x>`: acceleration in x direction in *m/s²*
1. `<acc y>`: acceleration in y direction in *m/s²*
1. `<acc z>`: acceleration in z direction in *m/s²*
1. `<gyr x>`: turn rate in x direction in *rad/s*
1. `<gyr y>`: turn rate in y direction in *rad/s*
1. `<gyr z>`: turn rate in z direction in *rad/s*


### Velocity Measurement

Velocity of the vehicle measured by wheel odometers,

Tag: `VELOCITY`

Structure: `VELOCITY,<timestamp>,<vel>`

Example: `VELOCITY,911635288,9.594444444444445`

Fields:

1. `<vel>`: velocity in x direction in *m/s*


### Steering Measurement

Steering angle of the front wheels measurement by a corresponding sensor.

Tag: `STEERING`

Structure: `STEERING,<timestamp>,<angle>,<rate>`

Example: `STEERING,911635288,0.01171059592244286,0`

Fields:

1. `<angle>`: steering angle in *rad*
1. `<rate>`: change of steering angle in *rad/s* (not used in paper)


### GNSS Measurement

Position measurement provided by the GNSS receiver.

Tag: `GNSS`

Structure: `GNSS,<timestamp>,<lat>,<lon>,<alt>,<quality>`

Example: `GNSS,911673399,0.8871484676876426,0.2254892526080403,350.9,8`

Fields:

1. `<lat>`: latitude in *rad*
1. `<lon>`: longitude in *rad*
1. `<alt>`: altitude in *m*
1. `<quality>`: solution quality reported by receiver (not present in all datasets):

    0. unknown/invalid
    1. no solution
    2. dead reckoning
    3. single
    4. SBAS
    5. DGPS/DGNSS
    6. PPP
    7. RTK float
    8. RTK fix

## Datasets

### Parking Lot

Driving on a parking lot with partially harsh maneuvers, including sharp accelerating and decelerating as well as high turning speeds.

* Filename: `parking_lot.csv`
* Duration: 11:11
* Distance: 3.01 km
* Median speed: 17.5 km/h
* Max. speed: 48.8 km/h

### Suburb

Driving through a suburb of Bremen, Germany, with comparably low speeds.

* Filename: `suburb.csv`
* Duration: 20:46
* Distance: 4.51 km
* Median speed: 13.8 km/h
* Max. speed: 51.0 km/h

### City

Driving in the inner city of Chemnitz, Germany, and has medium speeds.

* Filename: `city.csv`
* Duration: 13:19
* Distance: 5.52 km
* Median speed: 21.1 km/h
* Max. speed: 60.9 km/h

### Urban Freeway

Driving the majority of the time on an urban freeway in Chemnitz, Germany, with higher speeds.

* Filename: `ubran_freeway.csv`
* Duration: 42:28
* Distance: 25.80 km
* Median speed: 38.6 km/h
* Max. speed: 101.6 km/h


## Acknowledgments

The authors thank IAV GmbH, Department Automated Driving Functions, Germany, for providing the research vehicle and the test driver for recording the datasets "Parking Lot", "City", and "Urban Freeway" in Chemnitz.

This research was partially funded by German Aerospace Center (DLR) Space Administration with financial means of the German Federal Ministry for Economic Affairs and Climate Action (BMWK) on the basis of a decision by the German Bundestag, projects "OPA3L" (grant No. 50 NA 1909), "MUTIG-VORAN" (grant No. 50 NA 2202A), "Safety Control Center" (grant No. 50 NA 2302B), and "iMarEx" (grant No. 50 NA 2206A).
