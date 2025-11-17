# weatherData_Project

# DSAI3202 - Monthly Precipitation Prediction for the Netherlands  
**Phase I Submission – Medallion Architecture on Azure Databricks Lakehouse**  
Rasha Fadlalla (60301813) & Lana Mukhtar (60107216)

## Project Overview
Forecasting monthly total precipitation (mm) for the Netherlands using historical daily data from **De Bilt station (NLM00006260)** — the official KNMI reference station — from **2014 to 2022** (NOAA GHCN-Daily dataset).

We followed Lab 3 exactly and built a full **Bronze → Silver → Gold** lakehouse architecture on Azure.

## Data Source
- **NOAA GHCN-Daily** (Global Historical Climatology Network)
- Public S3 bucket: `s3://noaa-ghcn-pds/csv.gz/YYYY.csv.gz`
- Element filtered: **PRCP** (precipitation in tenths of mm)
- Station used: **NLM00006260** (De Bilt) — complete daily data 2014–2022

## Lakehouse Architecture (Exactly as Lab 3)

| Layer   | Location                                                                   | Format  | Description |
|---------|----------------------------------------------------------------------------|---------|-----------|
| Bronze  | `abfss://lakehouse@dsai3202weatherdata.dfs.core.windows.net/raw/daily_weather/` | CSV     | 9 raw filtered files (one per year, only De Bilt PRCP) |
| Silver  | `/silver/daily_prcp_debilt/`                                               | Delta   | Cleaned daily data: date parsed, PRCP converted to mm, year/month extracted |
| Gold    | `/gold/monthly_precipitation_debilt/`                                     | Delta   | Monthly total precipitation (mm) — ready for modeling and Power BI |

### Key Transformations
- Converted PRCP from tenths of mm → real mm (`value / 10`)
- Aggregated daily → monthly totals per year/month
- Final gold table: **108 rows** (9 years × 12 months)

## Files in This Repository
- `notebooks/DSAI3202_Weather_Lakehouse_Phase1.ipynb` → Complete Databricks notebook (bronze → silver → gold)
- `screenshots/` → Proof of all layers in storage + final monthly table
- `data_sample/` → Sample of raw data

## Next Steps (Phase II)
- Time-series modeling (Prophet / LSTM / SARIMA)
- Power BI dashboard with monthly trends and forecasts

**Phase I is fully complete and follows Lab 3 medallion architecture 100%.**

Thank you!  
Rasha & Lana – November 17, 2025
