# Carbon-Emission-Analysis
![image](https://github.com/user-attachments/assets/6f52ab70-159d-425f-9165-a1b6b6801573)

This report aims to analyze carbon emissions to examine the carbon footprint across various industries. We aim to identify sectors with the highest levels of emissions by analyzing them across countries and years, as well as to uncover trends.

Carbon emissions play a crucial role in the environment, accounting for over 75% of global emissions and posing a significant environmental challenge. These emissions contribute to the accumulation of greenhouse gases in the atmosphere, leading to climate change, planetary warming, and involvement in various environmental disasters.

Through this analysis, we hope to gain an understanding of the environmental impact of different industries and contribute to making informed decisions in sustainable development.
## Data Source: Where Our Data Comes From
Our dataset is compiled from publicly available data from nature.com and encompasses the product carbon footprints (PCF) for various companies. PCFs represent the greenhouse gas emissions associated with specific products, quantified in CO2 (carbon dioxide equivalent).

## Data Structure
The dataset consists of 4 tables containing information regarding carbon emissions generated during the production of goods.
![image](https://github.com/user-attachments/assets/8e138585-8d0c-42ee-b1a3-528701d1b098)
## Data Exploring
### Table 'product_emissions'
```sql
select *
from product_emissions
limit 10;
```
| id            | company_id | country_id | industry_group_id | year | product_name                                                    | weight_kg | carbon_footprint_pcf | upstream_percent_total_pcf                       | operations_percent_total_pcf                     | downstream_percent_total_pcf                     | 
| ------------: | ---------: | ---------: | ----------------: | ---: | --------------------------------------------------------------: | --------: | -------------------: | -----------------------------------------------: | -----------------------------------------------: | -----------------------------------------------: | 
| 10056-1-2014  | 82         | 28         | 2                 | 2014 | Frosted Flakes(R) Cereal                                        | 0.7485    | 2                    | 57.50                                            | 30.00                                            | 12.50                                            | 
| 10056-1-2015  | 82         | 28         | 15                | 2015 | "Frosted Flakes, 23 oz, produced in Lancaster, PA (one carton)" | 0.7485    | 2                    | 57.50                                            | 30.00                                            | 12.50                                            | 
| 10222-1-2013  | 83         | 28         | 8                 | 2013 | Office Chair                                                    | 20.68     | 73                   | 80.63                                            | 17.36                                            | 2.01                                             | 
| 10261-1-2017  | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1488                 | 30.65                                            | 5.51                                             | 63.84                                            | 
| 10261-2-2017  | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1818                 | 25.08                                            | 4.51                                             | 70.41                                            | 
| 10261-3-2017  | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 2274                 | 20.05                                            | 3.61                                             | 76.34                                            | 
| 10324-1-2016  | 15         | 16         | 19                | 2016 | KURALON  fiber                                                  | 1500      | 10000                | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | 
| 10418-1-2013  | 84         | 9          | 19                | 2013 | Portland Cement                                                 | 1000      | 1102                 | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | 
| 10661-10-2014 | 85         | 28         | 11                | 2014 | Regular Straight 505® Jeans – Steel (Water                      | 0.7665    | 15                   | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | 
| 10661-10-2015 | 85         | 28         | 6                 | 2015 | Regular Straight 505® Jeans – Steel (Water                      | 0.7665    | 15                   | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | 

### Table 'industry_groups'
```sql
select *
from companies
limit 10;
```
| id | company_name                                   | 
| -: | ---------------------------------------------: | 
| 1  | "Autodesk, Inc."                               | 
| 2  | "Casio Computer Co., Ltd."                     | 
| 3  | "Cisco Systems, Inc."                          | 
| 4  | "CNX Coal Resources, LP"                       | 
| 5  | "Coca-Cola Enterprises, Inc."                  | 
| 6  | "Compañía Española de Petróleos, S.A.U. CEPSA" | 
| 7  | "Daikin Industries, Ltd."                      | 
| 8  | "Elitegroup computer systems co., Ltd."        | 
| 9  | "Fuji Xerox Co., Ltd."                         | 
| 10 | "Gamesa Corporación Tecnológica, S.A."         | 

### Table 'countries'
```sql
select *
from countries
limit 10;
```
| id | country_name | 
| -: | -----------: | 
| 1  | Australia    | 
| 2  | Belgium      | 
| 3  | Brazil       | 
| 4  | Canada       | 
| 5  | Chile        | 
| 6  | China        | 
| 7  | Colombia     | 
| 8  | Finland      | 
| 9  | France       | 
| 10 | Germany      | 

### Find Duplicate
```sql
select *, count(*) as count_duplicate
from product_emissions
group by 
	id,
	company_id,
	country_id
	industry_group_id,
	year,
	product_name,
	weight_kg,
	carbon_footprint_pcf,
	upstream_percent_total_pcf,
	operations_percent_total_pcf,
	downstream_percent_total_pcf
having count(*) > 1;
```
171 dong trung lap

### 1. Which products contribute the most to carbon emissions? 
```sql
select product_name,round(avg(carbon_footprint_pcf))
from product_emissions
group by product_name
order by round(avg(carbon_footprint_pcf)) desc;
```
| product_name                                                                                                                       | round(avg(carbon_footprint_pcf)) | 
| ---------------------------------------------------------------------------------------------------------------------------------: | -------------------------------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 3718044                          | 
| Wind Turbine G132 5 Megawats                                                                                                       | 3276187                          | 
| Wind Turbine G114 2 Megawats                                                                                                       | 1532608                          | 
| Wind Turbine G90 2 Megawats                                                                                                        | 1251625                          | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687                           | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000                           | 
| TCDE                                                                                                                               | 99075                            | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 91000                            | 
| Mercedes-Benz S-Class (S 500)                                                                                                      | 85000                            | 
| Mercedes-Benz SL (SL 350)                                                                                                          | 72000                            | 

### 2. What are the industry groups of these products?
```sql
select p.product_name, i.industry_group, round(avg(p.carbon_footprint_pcf)) as 'carbon emission'
from product_emissions p
join industry_groups i on i.id=p.industry_group_id
group by product_name
order by round(avg(carbon_footprint_pcf)) desc
limit 10;
```
| product_name                                                                                                                       | industry_group                     | carbon emission | 
| ---------------------------------------------------------------------------------------------------------------------------------: | ---------------------------------: | --------------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | Electrical Equipment and Machinery | 3718044         | 
| Wind Turbine G132 5 Megawats                                                                                                       | Electrical Equipment and Machinery | 3276187         | 
| Wind Turbine G114 2 Megawats                                                                                                       | Electrical Equipment and Machinery | 1532608         | 
| Wind Turbine G90 2 Megawats                                                                                                        | Electrical Equipment and Machinery | 1251625         | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | Automobiles & Components           | 191687          | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | Materials                          | 167000          | 
| TCDE                                                                                                                               | Materials                          | 99075           | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | Automobiles & Components           | 91000           | 
| Mercedes-Benz S-Class (S 500)                                                                                                      | Automobiles & Components           | 85000           | 
| Mercedes-Benz SL (SL 350)                                                                                                          | Automobiles & Components           | 72000           | 

### 3. What are the industries with the highest contribution to carbon emissions?
```sql
select i.industry_group, sum(p.carbon_footprint_pcf) as 'Carbon Emission'
from industry_groups i
join product_emissions p on i.id=p.industry_group_id
group by i.industry_group
order by p.carbon_footprint_pcf desc
limit 10;
```
| industry_group                                                         | Carbon Emission | 
| ---------------------------------------------------------------------: | --------------: | 
| Automobiles & Components                                               | 2582264         | 
| "Pharmaceuticals, Biotechnology & Life Sciences"                       | 72486           | 
| Chemicals                                                              | 62369           | 
| Materials                                                              | 577595          | 
| Media                                                                  | 23017           | 
| "Mining - Iron, Aluminum, Other Metals"                                | 8181            | 
| Technology Hardware & Equipment                                        | 363776          | 
| Containers & Packaging                                                 | 2988            | 
| "Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber" | 8909            | 
| Commercial & Professional Services                                     | 5265            | 

### 4. What are the companies with the highest contribution to carbon emissions?
```sql
select c.company_name, p.carbon_footprint_pcf
from companies c
join product_emissions p on c.id=p.company_id
group by c.company_name
order by round(sum(p.carbon_footprint_pcf)) desc
limit 10;
```
| company_name                            | carbon_footprint_pcf | 
| --------------------------------------: | -------------------: | 
| "Gamesa Corporación Tecnológica, S.A."  | 1251625              | 
| Daimler AG                              | 57100                | 
| Volkswagen AG                           | 21725                | 
| "Mitsubishi Gas Chemical Company, Inc." | 200                  | 
| "Hino Motors, Ltd."                     | 191687               | 
| Arcelor Mittal                          | 7                    | 
| Weg S/A                                 | 53058                | 
| General Motors Company                  | 27588                | 
| "Lexmark International, Inc."           | 1616                 | 
| "Daikin Industries, Ltd."               | 3653                 | 

### 5. What are the countries with the highest contribution to carbon emissions?
```sql
select c.country_name, avg(p.carbon_footprint_pcf)
from product_emissions p
join countries c on c.id=p.country_id
group by c.country_name
order by p.carbon_footprint_pcf desc
limit 10;
```
| country_name | avg(p.carbon_footprint_pcf) | 
| -----------: | --------------------------: | 
| Germany      | 33600.3731                  | 
| South Korea  | 5665.6061                   | 
| Brazil       | 9407.6111                   | 
| Japan        | 4600.2606                   | 
| India        | 1535.8750                   | 
| Netherlands  | 2011.9143                   | 
| France       | 129.2857                    | 
| South Africa | 1119.2727                   | 
| Ireland      | 855.0000                    | 
| Indonesia    | 721.0000                    | 

### 6. What is the trend of carbon footprints (PCFs) over the years?
