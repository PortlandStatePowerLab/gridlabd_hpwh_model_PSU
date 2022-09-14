# Heat Pump Water Heater:
Heat Pump Water Heater (HPWH) is energy-efficient devices. Several federal laws have been passed to encourage their deployment as EWHs alternative. 
# GridLAB-D:
GridLAB-D is an open-source, power distribution system simulation tool that was developed by the U.S Department of Energy (DOE) at Pacific Northwest National Labrotary. Among other modules, GridLAB-D incorporates a residential module. The residential module facilitates end-use loads such as water heaters and houses.
# Developed HPWH Model in GridLAB-D:
The developed HPWH model is validated against a real HPWH unit at Portland State University (PSU), the PowerLab. The physical HPWH unit is A. O. Smith, 50 gallon, CTA-2045 equipped device. The development of the HPWH model is heavily dependant on one of the parameters provided by CTA-2045. This parameter is ''EnergyTake''
## EnergyTake:
The EnergyTake is the amount of energy that the HPWH would need to consume to heat the water in its tank to the temperature set point. Generally, when a water heater is in idle mode, it slowly loses energy. This is known as “idle losses” and results in a gradual increase in EnergyTake. EnergyTake increases rapidly when a water draw occurs, wherein hot water is removed from the tank and replaced with cold water from the household water supply. EnergyTake decreases when the water heater energy source turns on, and it is zero when the tank temperature equals the temperature set point, shown in the following Figure. 
![et_temp](https://user-images.githubusercontent.com/56623148/169650900-8e2e3f1a-be4f-4302-8aec-5ce903b20741.png)

Energytake is used to represent the average tank temperature. The EnergyTake is calculated internally wihtin the source code. Users will only see the tank temperature. However, GridLAB-D users may see the EnergyTake values by simply typing ''energytake'' within water heater object.

## Parameters Definitions:
The developed HPWH model uses already defined parameters from the original GridLAB-D repository (i.e water_demand, tank_setpoint, tank_volume, etc).  However, due to the HPWH complicated behavior, a few other parameters were defined. This section presents the newly defined parameters.
- **heating_element_capacity:** This variable defines the rated power of the resistive heating element. The physical HPWH unit has a heating_element_capacity of 4.5kW. The resistive heating element triggers **ONLY** if there is a large water draw. Otherwise the compressor triggers.
- **Heating Sources Variables:** The physical HPWH unit operates by alternating between two heating sources (the resistive heating element and the compressor). If the water temperature (Tw) drops significantly below the tank setpoint (tank_setpoint), then the resistive heating element triggers. The resistive heating element then rapidly heats the water, though not to the tank setpoint. When the water temperature (Tw) reaches a specific threshold, the resistive heating element turns OFF and the compressor triggers to heat the water to the tank setpoint. To model this behavior, three variables are defined, 
     
     - **compressor_min_threshold:** This variable defines the minimum threshold for the compressor. This is the default heating source and it operates as long as the water temperature is above $\approx$ 103F (or less than 2 kWh).
     - **compressor_max_threshold:** This variable defines the maximum threshold for the compressor. If the water temperature (Tw) drops below $\approx$ 103F (equivalent to 2 kWh), the compressor turns off and the resistive heating element triggers. 
     - **heating_element_min_threshold:** Once the resistive heating element triggers, it does **NOT** turn off until the water temperature (Tw) reaches $\approx$ 110F (equivalent to 1.1 kWh).


## Testing the Developed HPWH Model:
This repository also includes a testing file that allows user to test the developed HPWH model. Once this repository is cloned, run the "hpwh_testing.glm" file by using the following command:


```gridlabd hpwh_testing.glm```


Make sure the "wd_1.csv" file is in the same directory as the "hpwh_testing.glm" file.
