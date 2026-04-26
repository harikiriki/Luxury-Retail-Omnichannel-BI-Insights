# Luxury-Retail-Omnichannel-BI-Insights
End-to-end Power BI solution for the luxury retail sector. Features omnichannel analytics (ROPO effect), Single Customer View (SCV) modeling, and advanced DAX measures for executive and operational decision-making.

# 💎 Luxury Retail Omnichannel BI Suite: Bridging Digital & Physical Sales

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

> An end-to-end Business Intelligence solution designed for the luxury retail sector. This project demonstrates how integrating fragmented data (E-commerce, CRM, POS) into a Single Customer View (SCV) can quantify the ROPO effect (Research Online, Purchase Offline) and empower sales advisors with data-driven clienteling tools.

## 📌 1. Project Overview

**The Business Problem:** Luxury brands often struggle with data silos. While customers seamlessly transition between browsing online and buying in high-end boutiques, the data remains disconnected. This prevents accurate ROI measurement for digital marketing and limits the personalization capabilities of frontline staff.

**The Solution:**
A multi-layered Power BI architecture based on a Star Schema data model. The system processes synthetic omnichannel data to deliver actionable insights across three levels of management:
1. **Strategic (Board of Directors):** Tracking overall profitability and omnichannel synergy.
2. **Operational (Boutique Managers):** Managing store performance, product mix, and team effectiveness.
3. **Execution (Sales Advisors):** A mobile-optimized Customer 360 profile to drive personalized up-selling (Clienteling 2.0).

---

## 🏛️ 2. Data Architecture & Modeling

To ensure compliance with GDPR and corporate confidentiality, the entire dataset was synthetically generated using **Mockaroo** and **Python** scripts, meticulously parameterized to reflect real-world luxury retail distributions (e.g., high gross margins, Pareto principle in VIP segmentation).

* **Data Model:** Optimized Star Schema (1-to-Many relationships).
* **Core Tables:** `FACT_SALES`, `FACT_EVENT`, `DIM_CUSTOMERS`, `CALENDAR`.
* **Data Integration:** The model successfully links physical transactions with digital footprints (Web Traffic) using a unified `Customer_ID`, establishing a true **Single Customer View**.

---

## 📊 3. Dashboard Gallery & Business Logic

### A. Strategic Board View (Holistic Performance)
Designed for C-level executives to monitor macroeconomic indicators and omnichannel health.
* **Key Metrics:** Total Revenue, Gross Profit Margin (%), ROPO Coefficient.
* **Business Value:** Quantifies how digital touchpoints drive physical sales, enabling better allocation of marketing budgets.
* *screen*

### B. Boutique Manager View (Operational Excellence)
Built to help store managers optimize daily operations and monitor the effectiveness of their sales team.
* **Key Metrics:** Revenue per Advisor, Client Portfolio Structure (VIP vs. Occasional), Merchandising Mix (Treemap).
* **Business Value:** Instantly identifies if advisors are focusing on high-value clients and helps adjust Visual Merchandising based on real-time category performance.
* *screen*

### C. Clienteling 360° View (Mobile Interface)
A mobile-optimized dashboard designed for frontline workers (Sales Advisors) to use on mobile devices during client interactions.
* **Key Features:** Customer Lifetime Value (CLV), Digital Footprint tracking.
* **Business Value:** Eliminates information asymmetry. The advisor knows exactly what the client browsed online yesterday and receives an automated "Next Best Action" recommendation.
* *screen*

---

## ⚙️ 4. Highlighted Technical Implementation (DAX)

To simulate AI-driven product recommendations without a complex Machine Learning backend, I implemented a rule-based **Next Best Action** engine using DAX. 

```dax
Next_Best_Action_Recommendation = 
VAR LastCategory = 
    TOPN(
        1, 
        VALUES('FACT_SALES'[Product_Category]), 
        CALCULATE(MAX('FACT_SALES'[Purchase_Date]))
    )
RETURN
SWITCH( TRUE(),
    LastCategory = "Watches", "Suggest: Premium Watch Winder",
    LastCategory = "Leather Goods", "Suggest: Personalized Leather Keychain",
    LastCategory = "Ready-to-Wear", "Suggest: Silk Scarf Accessory",
    "Bestseller: Iconic Monogram Bag" -- Fallback for new clients
)
