# Heat Pump Water Heater:
Heat Pump Water Heater (HPWH) is energy-efficient devices. Several federal laws have been passed to encourage their deployment as EWHs alternative. 
# GridLAB-D:
GridLAB-D is an open-source, power distribution system simulation tool that was developed by the U.S Department of Energy (DOE) at Pacific Northwest National Labrotary. Among other modules, GridLAB-D incorporates a residential module. The residential module facilitates end-use loads such as water heaters and houses.
# Developed HPWH Model in GridLAB-D:
The developed HPWH model is validated against a real HPWH unit at Portland State University (PSU), the PowerLab. The physical HPWH unit is A. O. Smith, 50 gallon, CTA-2045 equipped device. The development of the HPWH is heavily dependant on one of the parameters provided by CTA-2045. This parameter is ''EnergyTake''
## EnergyTake:
The EnergyTake is the amount of energy that the HPWH would need to consume to heat the water in its tank to the temperature set point. Generally, when a water heater is in idle mode, it slowly loses energy. This is known as “idle losses” and results in a gradual increase in EnergyTake. EnergyTake increases rapidly when a water draw occurs, wherein hot water is removed from the tank and replaced with cold water from the household water supply. EnergyTake decreases when the water heater energy source turns on, and it is zero when the tank temperature equals the temperature set point, shown in the following Figure. 
![et_temp](https://user-images.githubusercontent.com/56623148/169650900-8e2e3f1a-be4f-4302-8aec-5ce903b20741.png)

Energytake is used to represent the average tank temperature. The EnergyTake is calculated internally wihtin the source code. Users will only see the tank temperature. However, GridLAB-D users may see the EnergyTake values by simply typing ''energytake'' within water heater object.
