# Data Dictionary: Weather-Energy Data Warehouse Project

This document provides detailed definitions for all variables in the datasets used in this project, including data types, units, descriptions, and derivation methods where applicable.

## 1. Weather Dataset (weather_clean.rds)

### Location Variables
| Variable | Type | Description |
|----------|------|-------------|
| location_name | character | Full name of the location (City, State format) |
| city | character | Name of the city |
| state | character | Two-letter state abbreviation |
| latitude_deg | numeric | Latitude in decimal degrees |
| longitude_deg | numeric | Longitude in decimal degrees |

### Time Variables
| Variable | Type | Description |
|----------|------|-------------|
| datetime_utc | POSIXct | Date and time in UTC |
| date | Date | Calendar date |
| year | integer | Year of observation |
| month | integer | Month of observation (1-12) |
| day | integer | Day of month (1-31) |
| hour | integer | Hour of day (0-23) |
| weekday | factor | Day of week (Mon-Sun) |
| season | factor | Season (Winter, Spring, Summer, Fall) |
| time_of_day | factor | Period of day (Morning, Afternoon, Evening, Night) |

### Weather Measurements
| Variable | Type | Description | Units |
|----------|------|-------------|-------|
| temperature_c | numeric | Temperature | Celsius |
| temperature_f | numeric | Temperature | Fahrenheit |
| humidity_pct | numeric | Relative humidity | Percentage |
| precipitation_mm | numeric | Precipitation amount | Millimeters |
| wind_speed_mps | numeric | Wind speed | Meters per second |
| cloud_cover_pct | numeric | Cloud cover | Percentage |
| heat_index_f | numeric | Heat index | Fahrenheit |

### Categorical Variables
| Variable | Type | Description |
|----------|------|-------------|
| precipitation_category | factor | Precipitation intensity (None, Light, Moderate, Heavy, Extreme) |
| wind_category | factor | Wind intensity based on Beaufort scale |
| weather_condition | factor | Overall weather condition (Snow/Freezing Rain, Rain, Overcast, Partly Cloudy, Clear) |
| is_extreme_heat | logical | Flag indicating extreme heat (temperature > 95°F) |
| is_extreme_cold | logical | Flag indicating extreme cold (temperature < 20°F) |
| is_heavy_precipitation | logical | Flag indicating heavy precipitation (> 10mm) |

## 2. Energy Dataset (energy_clean.rds)

### Company Variables
| Variable | Type | Description |
|----------|------|-------------|
| company_code | character | Unique identifier for energy company/region |
| company_name | character | Full name of energy company/region |
| state | character | Primary state of operation |
| region | character | Geographic region (Texas, California, New York, etc.) |
| company_size | factor | Categorization by energy volume (Small, Medium, Large, Very Large) |

### Time Variables
| Variable | Type | Description |
|----------|------|-------------|
| date | Date | Observation date |
| year | integer | Year of observation |
| month | integer | Month of observation (1-12) |
| day | integer | Day of month (1-31) |
| weekday | factor | Day of week (Mon-Sun) |
| season | factor | Season (Winter, Spring, Summer, Fall) |
| season_peak | factor | Peak/Off-Peak season designation |
| quarter | character | Calendar quarter (Q1-Q4) |
| day_type | factor | Weekday or Weekend |

### Measurement Variables
| Variable | Type | Description |
|----------|------|-------------|
| measurement_type | character | Type code for energy measurement |
| measurement_name | character | Descriptive name of energy measurement |
| measurement_category | factor | Category of measurement (Generation, Demand, Interchange, Other) |
| measurement_subcategory | factor | Detailed categorization of measurement |
| value_numeric | numeric | Numerical energy value |
| units | character | Units of measurement |
| value | character | Original value string from API |
| timezone | character | Time zone code |
| timezone_desc | character | Time zone description |
| value_conversion_failed | logical | Flag indicating numeric conversion issues |

## 3. Merged Dataset (merged_data.rds)

### Location Variables
| Variable | Type | Description |
|----------|------|-------------|
| location | character | Weather station location (City, State) |
| latitude | numeric | Latitude in decimal degrees |
| longitude | numeric | Longitude in decimal degrees |
| state | character | Two-letter state abbreviation |

### Weather Variables
| Variable | Type | Description | Units |
|----------|------|-------------|-------|
| temp_mean | numeric | Average daily temperature | Fahrenheit |
| temp_min | numeric | Minimum daily temperature | Fahrenheit |
| temp_max | numeric | Maximum daily temperature | Fahrenheit |
| temp_range | numeric | Daily temperature range (max-min) | Fahrenheit |
| humidity_mean | numeric | Average daily humidity | Percentage |
| precipitation_total | numeric | Total daily precipitation | Millimeters |
| wind_speed_mean | numeric | Average daily wind speed | Meters per second |
| wind_speed_max | numeric | Maximum daily wind speed | Meters per second |
| cloud_cover_mean | numeric | Average daily cloud cover | Percentage |
| cooling_degree_days | numeric | Cooling degree days (base 65°F) | Degree days |
| heating_degree_days | numeric | Heating degree days (base 65°F) | Degree days |
| hourly_records | integer | Number of hourly observations |

### Energy Variables
| Variable | Type | Description |
|----------|------|-------------|
| energy_region | character | Energy region code |
| energy_region_full_name | character | Full name of energy region |
| period | character | Date in string format |
| respondent-name | character | Name of responding entity |
| type | character | Energy measurement type code |
| type-name | character | Name of energy measurement type |
| timezone | character | Time zone of energy measurement |
| timezone-description | character | Description of time zone |
| value | character | Energy value (string) |
| value-units | character | Units of energy measurement |
| energy_value | numeric | Numeric energy value |
| energy_type | factor | Simplified energy type (Demand, Net Generation, Total Interchange) |

### Derived Analysis Variables
| Variable | Type | Description |
|----------|------|-------------|
| month | factor | Month of observation (Jan-Dec) |
| season | factor | Season (Winter, Spring, Summer, Fall) |
| weekday | factor | Day of week (Mon-Sun) |
| is_weekend | logical | Flag for weekend days |
| weather_condition | factor | Weather condition category |
| temp_category | factor | Temperature range category |
| temp_squared | numeric | Squared temperature (for U-curve analysis) |
| temp_centered | numeric | Centered temperature value |
| temp_centered_squared | numeric | Squared centered temperature |
| log_energy | numeric | Natural log of energy value |

## 4. Derived Datasets

### Daily Weather Aggregates (weather_daily.rds)
Contains daily aggregations of the hourly weather data with additional derived metrics.

### State-level Energy Aggregates (energy_by_state.rds)
Contains state-level aggregations of energy data with pivoted measurement categories.

### Region-level Energy Aggregates (energy_by_region.rds)
Contains region-level aggregations of energy data for broader geographic analysis.

## Notes on Data Sources

1. **Weather Data Source**: Open-Meteo ERA5 Historical Weather API
   - Access: https://archive-api.open-meteo.com/v1/era5
   - Coverage: 20 major U.S. cities
   - Time Range: January 1, 2024 - December 31, 2024
   - Temporal Resolution: Hourly

2. **Energy Data Source**: U.S. Energy Information Administration (EIA) API
   - Access: https://api.eia.gov/v2/electricity/rto/daily-region-data/data/
   - Coverage: U.S. energy regions and companies
   - Time Range: January 1, 2024 - December 31, 2024
   - Temporal Resolution: Daily

## Data Transformations

1. **Temperature Conversions**: Celsius to Fahrenheit using the formula: °F = (°C × 9/5) + 32

2. **Heat Index Calculation**: Uses the NOAA heat index formula for temperatures above 80°F

3. **Cooling/Heating Degree Days**: Calculated using a base temperature of 65°F:
   - Cooling degree days = max(0, average temperature - 65°F)
   - Heating degree days = max(0, 65°F - average temperature)

4. **Weather Categorization**: Based on standard meteorological thresholds for precipitation and cloud cover

5. **Energy Region Mapping**: Custom mapping table connecting weather locations to energy regions based on geographic proximity and service territories