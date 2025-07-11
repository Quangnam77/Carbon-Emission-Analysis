# Carbon-Emission-Analysis
What is the project about?

![image](https://github.com/user-attachments/assets/66353940-22df-4f35-9bce-197eb2fe3f84)

This report aims to analyze carbon emissions to examine the carbon footprint across various industries. We aim to identify sectors with the highest levels of emissions by analyzing them across countries and years, as well as to uncover trends.

Carbon emissions play a crucial role in the environment, accounting for over 75% of global emissions and posing a significant environmental challenge. These emissions contribute to the accumulation of greenhouse gases in the atmosphere, leading to climate change, planetary warming, and involvement in various environmental disasters.

Through this analysis, we hope to gain an understanding of the environmental impact of different industries an
## Data Source
Our dataset is compiled from publicly available data from nature.com and encompasses the product carbon footprints (PCF) for various companies. PCFs represent the greenhouse gas emissions associated with specific products, quantified in CO2 (carbon dioxide equivalent).
## Data structure
The dataset consists of 4 tables containing information regarding carbon emissions generated during the production of goods.
![image](https://github.com/user-attachments/assets/e875be19-9cb7-4f52-8bc6-a2db629d8ec9)

## Data exploring
### Table: Product_emissions
```sql
SELECT *
FROM product_emissions
LIMIT 10;
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
### table: Industry_groups
```sql
SELECT *
FROM industry_groups
LIMIT 10;
```
| id | industry_group                                                         | 
| -: | ---------------------------------------------------------------------: | 
| 1  | "Consumer Durables, Household and Personal Products"                   | 
| 2  | "Food, Beverage & Tobacco"                                             | 
| 3  | "Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber" | 
| 4  | "Mining - Iron, Aluminum, Other Metals"                                | 
| 5  | "Pharmaceuticals, Biotechnology & Life Sciences"                       | 
| 6  | "Textiles, Apparel, Footwear and Luxury Goods"                         | 
| 7  | Automobiles & Components                                               | 
| 8  | Capital Goods                                                          | 
| 9  | Chemicals                                                              | 
| 10 | Commercial & Professional Services                                     | 
### Table: companies
```sql
SELECT *
FROM companies
LIMIT 10;
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
### Table: countries
```sql
SELECT *
FROM countries
LIMIT 10;
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

## Find duplicate
```sql
SELECT *, Count(*) AS count_duplicate
FROM product_emissions
GROUP BY
	id,	
	company_id,	
	country_id,	
	industry_group_id,	
	year,	
	product_name,	
	weight_kg,	
	carbon_footprint_pcf,	
	upstream_percent_total_pcf,	
	operations_percent_total_pcf,	
	downstream_percent_total_pcf
HAVING Count(*) > 1;
```
Result
Received: 171 rows
| id           | company_id | country_id | industry_group_id | year | product_name                                                    | weight_kg | carbon_footprint_pcf | upstream_percent_total_pcf                       | operations_percent_total_pcf                     | downstream_percent_total_pcf                     | count_duplicate | 
| -----------: | ---------: | ---------: | ----------------: | ---: | --------------------------------------------------------------: | --------: | -------------------: | -----------------------------------------------: | -----------------------------------------------: | -----------------------------------------------: | --------------: | 
| 10056-1-2014 | 82         | 28         | 2                 | 2014 | Frosted Flakes(R) Cereal                                        | 0.7485    | 2                    | 57.50                                            | 30.00                                            | 12.50                                            | 2               | 
| 10056-1-2015 | 82         | 28         | 15                | 2015 | "Frosted Flakes, 23 oz, produced in Lancaster, PA (one carton)" | 0.7485    | 2                    | 57.50                                            | 30.00                                            | 12.50                                            | 2               | 
| 10222-1-2013 | 83         | 28         | 8                 | 2013 | Office Chair                                                    | 20.68     | 73                   | 80.63                                            | 17.36                                            | 2.01                                             | 2               | 
| 10261-1-2017 | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1488                 | 30.65                                            | 5.51                                             | 63.84                                            | 2               | 
| 10261-2-2017 | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 1818                 | 25.08                                            | 4.51                                             | 70.41                                            | 2               | 
| 10261-3-2017 | 14         | 16         | 25                | 2017 | Multifunction Printers                                          | 110       | 2274                 | 20.05                                            | 3.61                                             | 76.34                                            | 2               | 
| 10324-1-2016 | 15         | 16         | 19                | 2016 | KURALON  fiber                                                  | 1500      | 10000                | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | 2               | 
| 10418-1-2013 | 84         | 9          | 19                | 2013 | Portland Cement                                                 | 1000      | 1102                 | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | 2               | 
| 10661-1-2014 | 85         | 28         | 11                | 2014 | 501® Original Jeans – Dark Stonewash                            | 0.997     | 16                   | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | 2               | 
| 10661-1-2015 | 85         | 28         | 6                 | 2015 | 501® Original Jeans – Dark Stonewash                            | 0.997     | 16                   | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | N/a (product with insufficient stage-level data) | 2               | 
### Which products contribute the most to carbon emissions?
```sql
SELECT 
	product_name, 
	ROUND(AVG(carbon_footprint_pcf),2) AS "carbon emissions"
FROM product_emissions pe
GROUP BY (pe.product_name )
ORDER BY ROUND(AVG(carbon_footprint_pcf),2) DESC
LIMIT 10;
```
Result
|product_name|carbon emissions|
|------------|----------------|
|Wind Turbine G128 5 Megawats|3718044.00|
|Wind Turbine G132 5 Megawats|3276187.00|
|Wind Turbine G114 2 Megawats|1532608.00|
|Wind Turbine G90 2 Megawats|1251625.00|
|Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.|191687.00|
|Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall|167000.00|
|TCDE|99075.00|
|Mercedes-Benz GLE (GLE 500 4MATIC)|91000.00|
|Mercedes-Benz S-Class (S 500)|85000.00|
|Mercedes-Benz SL (SL 350)|72000.00|
### What are the industry groups of these products?
```sql
SELECT 
	product_name, 
	ROUND(AVG(carbon_footprint_pcf),2) AS "carbon emissions",
	industry_groups.industry_group 
FROM product_emissions pe
JOIN industry_groups ON pe.industry_group_id = industry_groups.id
GROUP BY (pe.product_name )
ORDER BY ROUND(AVG(carbon_footprint_pcf),2) DESC
LIMIT 10;
```
Result
|product_name|carbon emissions|industry_group|
|------------|----------------|--------------|
|Wind Turbine G128 5 Megawats|3718044.00|Electrical Equipment and Machinery|
|Wind Turbine G132 5 Megawats|3276187.00|Electrical Equipment and Machinery|
|Wind Turbine G114 2 Megawats|1532608.00|Electrical Equipment and Machinery|
|Wind Turbine G90 2 Megawats|1251625.00|Electrical Equipment and Machinery|
|Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.|191687.00|Automobiles & Components|
|Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall|167000.00|Materials|
|TCDE|99075.00|Materials|
|Mercedes-Benz GLE (GLE 500 4MATIC)|91000.00|Automobiles & Components|
|Mercedes-Benz S-Class (S 500)|85000.00|Automobiles & Components|
|Mercedes-Benz SL (SL 350)|72000.00|Automobiles & Components|
There are three industry groups have the most carbon emissions: Electrical Equipment and Machinery, Automobiles & Components, Materials
### What are the industries with the highest contribution to carbon emissions?
```sql
SELECT 
	industry_groups.industry_group, 	
	ROUND(SUM(carbon_footprint_pcf),2) AS "carbon emissions"
FROM product_emissions pe
JOIN industry_groups ON pe.industry_group_id = industry_groups.id
GROUP BY (industry_groups.industry_group )
ORDER BY ROUND(SUM(carbon_footprint_pcf),2) DESC
LIMIT 10;
```
Result
|industry_group|carbon emissions|
|--------------|----------------|
|Electrical Equipment and Machinery|9801558.00|
|Automobiles & Components|2582264.00|
|Materials|577595.00|
|Technology Hardware & Equipment|363776.00|
|Capital Goods|258712.00|
|"Food, Beverage & Tobacco"|111131.00|
|"Pharmaceuticals, Biotechnology & Life Sciences"|72486.00|
|Chemicals|62369.00|
|Software & Services|46544.00|
|Media|23017.00|
### What are the companies with the highest contribution to carbon emissions?
```sql
SELECT 
	c.company_name, 	 
	ROUND(SUM(carbon_footprint_pcf),2) AS "carbon emissions"
FROM product_emissions pe
JOIN companies c  ON pe.company_id  = c.id
GROUP BY (c.company_name )
ORDER BY ROUND(SUM(carbon_footprint_pcf),2) DESC
LIMIT 10;
```
Result
|company_name|carbon emissions|
|------------|----------------|
|"Gamesa Corporación Tecnológica, S.A."|9778464.00|
|Daimler AG|1594300.00|
|Volkswagen AG|655960.00|
|"Mitsubishi Gas Chemical Company, Inc."|212016.00|
|"Hino Motors, Ltd."|191687.00|
|Arcelor Mittal|167007.00|
|Weg S/A|160655.00|
|General Motors Company|137007.00|
|"Lexmark International, Inc."|132012.00|
|"Daikin Industries, Ltd."|105600.00|
### What are the countries with the highest contribution to carbon emissions?
```sql
SELECT 
	c.country_name , 	 
	ROUND(SUM(carbon_footprint_pcf),2) AS "carbon emissions"
FROM product_emissions pe
JOIN countries c   ON pe.company_id  = c.id
GROUP BY (c.country_name  )
ORDER BY ROUND(SUM(carbon_footprint_pcf),2) DESC
LIMIT 10;
```
Result
|country_name|carbon emissions|
|------------|----------------|
|Germany|9778464.00|
|Lithuania|212016.00|
|Greece|191687.00|
|Japan|132012.00|
|Colombia|105600.00|
|South Africa|35505.00|
|France|21364.00|
|Italy|20000.00|
|Ireland|11160.00|
|India|9328.00|
### What is the trend of carbon footprints (PCFs) over the years?
```sql
SELECT
    pe.year,
    ROUND(SUM(carbon_footprint_pcf),2) AS "carbon emissions"
FROM product_emissions pe
GROUP BY (pe.`year`);
```
Result
|year|carbon emissions|
|----|----------------|
|2013|503857.00|
|2014|624226.00|
|2015|10840415.00|
|2016|1640182.00|
|2017|340271.00|
### Which industry groups has demonstrated the most notable decrease in carbon footprints (PCFs) over time?
```sql
SELECT
    pe.year,
    ig.industry_group,
    ROUND(SUM(carbon_footprint_pcf),2) AS "carbon emissions"
FROM product_emissions pe
JOIN industry_groups ig ON pe.industry_group_id = ig.id
GROUP BY pe.`year`, ig.industry_group
ORDER BY pe.year;
```
Result 
|year|industry_group|carbon emissions|
|----|--------------|----------------|
|2013|"Food, Beverage & Tobacco"|4995.00|
|2013|"Pharmaceuticals, Biotechnology & Life Sciences"|32271.00|
|2013|Automobiles & Components|130189.00|
|2013|Capital Goods|60190.00|
|2013|Commercial & Professional Services|1157.00|
|2013|Consumer Durables & Apparel|2867.00|
|2013|Energy|750.00|
|2013|Household & Personal Products|0.00|
|2013|Materials|200513.00|
|2013|Media|9645.00|
|2013|Software & Services|6.00|
|2013|Technology Hardware & Equipment|61100.00|
|2013|Telecommunication Services|52.00|
|2013|Utilities|122.00|
|2014|"Food, Beverage & Tobacco"|2685.00|
|2014|"Pharmaceuticals, Biotechnology & Life Sciences"|40215.00|
|2014|Automobiles & Components|230015.00|
|2014|Capital Goods|93699.00|
|2014|Commercial & Professional Services|477.00|
|2014|Consumer Durables & Apparel|3280.00|
|2014|Food & Staples Retailing|773.00|
|2014|Materials|75678.00|
|2014|Media|9645.00|
|2014|Retailing|19.00|
|2014|Semiconductors & Semiconductor Equipment|50.00|
|2014|Software & Services|146.00|
|2014|Technology Hardware & Equipment|167361.00|
|2014|Telecommunication Services|183.00|
|2015|"Consumer Durables, Household and Personal Products"|931.00|
|2015|"Food, Beverage & Tobacco"|0.00|
|2015|"Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber"|8909.00|
|2015|"Mining - Iron, Aluminum, Other Metals"|8181.00|
|2015|"Textiles, Apparel, Footwear and Luxury Goods"|387.00|
|2015|Automobiles & Components|817227.00|
|2015|Capital Goods|3505.00|
|2015|Chemicals|62369.00|
|2015|Containers & Packaging|2988.00|
|2015|Electrical Equipment and Machinery|9801558.00|
|2015|Food & Beverage Processing|141.00|
|2015|Food & Staples Retailing|706.00|
|2015|Gas Utilities|122.00|
|2015|Media|1919.00|
|2015|Retailing|11.00|
|2015|Semiconductors & Semiconductors Equipment|3.00|
|2015|Software & Services|22856.00|
|2015|Technology Hardware & Equipment|106157.00|
|2015|Telecommunication Services|183.00|
|2015|Tires|2022.00|
|2015|Tobacco|1.00|
|2015|Trading Companies & Distributors and Commercial Services & Supplies|239.00|
|2016|"Food, Beverage & Tobacco"|100289.00|
|2016|Automobiles & Components|1404833.00|
|2016|Capital Goods|6369.00|
|2016|Commercial & Professional Services|2890.00|
|2016|Consumer Durables & Apparel|1162.00|
|2016|Energy|10024.00|
|2016|Food & Staples Retailing|2.00|
|2016|Materials|88267.00|
|2016|Media|1808.00|
|2016|Semiconductors & Semiconductor Equipment|4.00|
|2016|Software & Services|22846.00|
|2016|Technology Hardware & Equipment|1566.00|
|2016|Utilities|122.00|
|2017|"Food, Beverage & Tobacco"|3162.00|
|2017|Capital Goods|94949.00|
|2017|Commercial & Professional Services|741.00|
|2017|Materials|213137.00|
|2017|Software & Services|690.00|
|2017|Technology Hardware & Equipment|27592.00|
### Which industry groups has demonstrated the most notable decrease in carbon footprints (PCFs) over time?
```sql
SELECT
ig.industry_group AS "Industry Group",
ROUND(SUM(CASE WHEN pe.year=2013 THEN pe.carbon_footprint_pcf ELSE 0 END),2) AS "2013 Emission",
ROUND(SUM(CASE WHEN pe.year=2014 THEN pe.carbon_footprint_pcf ELSE 0 END),2) AS "2014 Emission",
ROUND(SUM(CASE WHEN pe.year=2015 THEN pe.carbon_footprint_pcf ELSE 0 END),2) AS "2015 Emission",
ROUND(SUM(CASE WHEN pe.year=2016 THEN pe.carbon_footprint_pcf ELSE 0 END),2) AS "2016 Emission",
ROUND(SUM(CASE WHEN pe.year=2017 THEN pe.carbon_footprint_pcf ELSE 0 END),2) AS "2017 Emission"
FROM product_emissions AS pe
LEFT JOIN industry_groups AS ig ON ig.id = pe.industry_group_id
GROUP BY ig.industry_group
ORDER BY
"2017 Emission",
"2016 Emission",
"2015 Emission",
"2014 Emission",
"2013 Emission";
```
Result
|Industry Group|2013 Emission|2014 Emission|2015 Emission|2016 Emission|2017 Emission|
|--------------|-------------|-------------|-------------|-------------|-------------|
|"Food, Beverage & Tobacco"|4995.00|2685.00|0.00|100289.00|3162.00|
|Food & Beverage Processing|0.00|0.00|141.00|0.00|0.00|
|Capital Goods|60190.00|93699.00|3505.00|6369.00|94949.00|
|Technology Hardware & Equipment|61100.00|167361.00|106157.00|1566.00|27592.00|
|Materials|200513.00|75678.00|0.00|88267.00|213137.00|
|Consumer Durables & Apparel|2867.00|3280.00|0.00|1162.00|0.00|
|"Textiles, Apparel, Footwear and Luxury Goods"|0.00|0.00|387.00|0.00|0.00|
|Software & Services|6.00|146.00|22856.00|22846.00|690.00|
|Chemicals|0.00|0.00|62369.00|0.00|0.00|
|Semiconductors & Semiconductor Equipment|0.00|50.00|0.00|4.00|0.00|
|Commercial & Professional Services|1157.00|477.00|0.00|2890.00|741.00|
|Retailing|0.00|19.00|11.00|0.00|0.00|
|Utilities|122.00|0.00|0.00|122.00|0.00|
|Gas Utilities|0.00|0.00|122.00|0.00|0.00|
|Telecommunication Services|52.00|183.00|183.00|0.00|0.00|
|Electrical Equipment and Machinery|0.00|0.00|9801558.00|0.00|0.00|
|Containers & Packaging|0.00|0.00|2988.00|0.00|0.00|
|"Mining - Iron, Aluminum, Other Metals"|0.00|0.00|8181.00|0.00|0.00|
|Media|9645.00|9645.00|1919.00|1808.00|0.00|
|Automobiles & Components|130189.00|230015.00|817227.00|1404833.00|0.00|
|"Pharmaceuticals, Biotechnology & Life Sciences"|32271.00|40215.00|0.00|0.00|0.00|
|Tires|0.00|0.00|2022.00|0.00|0.00|
|Trading Companies & Distributors and Commercial Services & Supplies|0.00|0.00|239.00|0.00|0.00|
|"Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber"|0.00|0.00|8909.00|0.00|0.00|
|"Consumer Durables, Household and Personal Products"|0.00|0.00|931.00|0.00|0.00|
|Energy|750.00|0.00|0.00|10024.00|0.00|
|Food & Staples Retailing|0.00|773.00|706.00|2.00|0.00|
|Household & Personal Products|0.00|0.00|0.00|0.00|0.00|
|Tobacco|0.00|0.00|1.00|0.00|0.00|
|Semiconductors & Semiconductors Equipment|0.00|0.00|3.00|0.00|0.00|
