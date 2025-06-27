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
	product_name, 
	ROUND(SUM(carbon_footprint_pcf),2) AS "carbon emissions"
FROM product_emissions pe
JOIN industry_groups ON pe.industry_group_id = industry_groups.id
GROUP BY (industry_groups.industry_group )
ORDER BY ROUND(SUM(carbon_footprint_pcf),2) DESC
LIMIT 10;
```
Result
|industry_group|product_name|carbon emissions|
|--------------|------------|----------------|
|Electrical Equipment and Machinery|ACTI9 IID K 2P 40A 30MA AC-TYPE RESIDUAL CURRENT CIRCUIT BREAKER|9801558.00|
|Automobiles & Components|VW Polo V 1.6 TDI BlueMotion Technology|2582264.00|
|Materials|KURALON  fiber|577595.00|
|Technology Hardware & Equipment|Multifunction Printers|363776.00|
|Capital Goods|Office Chair|258712.00|
|"Food, Beverage & Tobacco"|Frosted Flakes(R) Cereal|111131.00|
|"Pharmaceuticals, Biotechnology & Life Sciences"|Alliance HPLC (High Peformance Liquid Chromatography)  The Alliance is an HPLC that is unique in that it has a single set of electronic boards that control the functions for both the solvent delivery system and the autosampler in the liquid chromatograph.|72486.00|
|Chemicals|Mobile Batteries|62369.00|
|Software & Services|USB software|46544.00|
|Media|"Bloomberg's standard-issue flat panel configuration (prior to 2010) was two 19\" panels mounted on a metal stand. In early 2010 Bloomberg engaged in the WRI Product Life Cycle Roadtest for this functional unit (cradle-to-grave). The functional unit has a lifespan of 5 years, so the emissions indicated [in this report] are the full emissions associated with that lifespan."|23017.00|
### What are the companies with the highest contribution to carbon emissions?
