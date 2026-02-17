DLIT Simulation Specification

1. Purpose
Simulate how a Dynamic Local Income Tax (DLIT) on new incoming high earners affects migration patterns and housing costs in Bay Area cities. 

Primary Question: Does DLIT reduce high-income inflows and slow the rate of rent growth in the cities surrounding San Francisco. 


2. Units
- Agents: Households
- Locations: Cities
- Time Step: Monthly
- Horizon: 5 years (60 months)


3. Cities
Cities included:
- San Francisco (origin)
- Daly City
- South San Francisco
- Brisbane
- Pacifica
- San Leandro
- Oakland
- Berkeley
- Alameda
- San Bruno
- San Rafael
- Sausalito
- Mill Valley

For each city, track:
- rent
- median income
- housing stock
- supply elasticity
- amenity score


4. Households 
Each household has:
- income
- current city
- month moved

Assumptions:
- Household income is fixed over time
- Households start in SF


5. Migration Process
    1. A fixed share of households consider moving
    2. Movers choose a destination city using a utility function
    3. Utility depends on:
    - rent
    - amenities
    - DLIT cost (if applicable)
    4. Movers relocate and become new residents of the destination city


6. DLIT Policy
Eligibility:
- must be a new mover
- destination city must be treated
- income is above city median

Tax Rule:
- Income multiple r = income/city median income
- Brackets:
    r <= 1: 0%
    1 < r < 2: 2%
    2 < r < 3: 4%
    r > 3: 6%

Duration
- DLIT policy will be implemented over a 5 year period
- DLIT applies to each new mover for the first 24 months after relocation

7. Housing Market Response
Each month:
- Compute inflow to each city
- Rent update rule:
%Δrent = α * (inflow/housing stock) / elasticity
    α (calibration parameter): controls the speed of rent adjustment
    α = 0.10 
    We test robustness for α ∈ [0.05, 0.20]


8. Outputs to Save
Per city, per month:
- population
- inflow
- outflow
- rent prices
- DLIT revenue

Key comparisons:
- Baseline vs DLIT
- Rent growth paths
- High-income inflow differences

9. Simplifications/Limitations
- No endogenous housing construction
- No wage changes
- Synthetic households

10. Data
    1. Median Household Income -- 2023 ACS 5 Year Estimates Data Profiles
    2. Housing Supply -- 2023 ACS 5 Year Estimates Data Profiles
    3. Home Price -- Zillow Home Value Index (ZHVI) (November 2025)

11. Variable Construction and Definitions
    1. Rent Growth Acceleration (outcome): 
        - difference between the average post-period rent growth and the average baseline rent growth. This measure captures changes in the trajectory of rent rates, giving us insight into how the rate of rent growth has changed over time. 
        - positive values indicate that rent is increasing faster than before, while negative values indicate a slowdown in growth compared to pre-existing trends.
        - isolates new housing market pressures  
        - post_growth - baseline_growth
    2. Baseline Rent Growth
        - average rent growth rate prior to the pandemic (Jan 2019- Feb 2020)
        - controls for pre-existing market trends (before remote work, COVID, migration shifts)
    3. Rent-to-Income Ratio
        - median_rent(Nov 2025) * 12/median household income
        - indicates the share of income that goes towards rent
        - measures affordability constraints and vulnerability to demand shocks
    4. Median Household Income
        - proxy for local purchasing power
    5. Housing Supply
        - captures the ability of a city to absorb new demand without accelerating rents 
