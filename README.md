# ev-fleet-analytics-for-risk-management
Python-based analysis of electric vehicle telematics data to identify driver default risk, operational hotspots, and key locations using DBSCAN clustering and geospatial techniques.
# Client Project: EV Fleet Analytics for Risk & Operations Management

## 1. Client Challenge / Business Problem

A key player in the electric vehicle (EV) financing sector was grappling with operational inefficiencies and rising financial risk due to a lack of actionable insights from their vehicle telematics data. While they collected vast amounts of GPS and battery data, it was too noisy and raw to be used effectively.

The client commissioned me to develop a data-driven solution to address three primary pain points:
*   **High Loan Default Rates:** The collections team had no reliable way to identify at-risk drivers before they defaulted, leading to significant financial losses.
*   **Ineffective Collections:** Without knowing drivers' primary residences or charging habits, communication and vehicle repossession efforts were inefficient and costly.
*   **Untapped Strategic Insights:** The company lacked a clear understanding of their fleet's operational hotspots, hindering strategic decisions about market expansion and resource allocation.

## 2. Project Goal & Scope

I was contracted to design, develop, and deliver a bespoke data analytics solution in Python. The primary objective was to transform raw telematics data into a suite of actionable intelligence tools to empower the client's collections, risk, and strategy teams.

The scope of the project included delivering four key analytical modules:
1.  **Driver Residence Identification:** Pinpoint the most likely home location for each vehicle operator.
2.  **Charging Behavior Analysis:** Identify primary charging locations for the fleet.
3.  **Proactive Risk Scoring:** Build a model to flag drivers exhibiting behavior correlated with a high risk of loan default.
4.  **Operational Hotspot Mapping:** Discover and visualize high-density zones of fleet activity.

## 3. Technology Stack
*   **Data Analysis & Manipulation:** Python, Pandas, NumPy
*   **Unsupervised Machine Learning:** Scikit-learn (DBSCAN Algorithm)
*   **Geospatial Processing:** Geopy, Haversine
*   **Reporting & Visualization:** Matplotlib, Seaborn, Folium (for interactive maps), Plotly
*   **Development Environment:** Jupyter Notebook

## 4. The Solution: A Phased Analytical Pipeline

I developed and implemented a robust, multi-phased pipeline to process the data and generate the required insights.

### Phase 0: Data Engineering & Cleansing
This foundational phase ensured the integrity and reliability of all subsequent analyses. The pipeline automated the detection and correction of data anomalies, including:
*   **Outlier Removal:** Filtering out invalid GPS coordinates and data points outside the client's core operational area (India).
*   **Anomaly Detection:** Programmatically flagging impossible speed-based "jumps" between data points and physically improbable battery level changes using domain-specific rules.
*   **Time-Series Imputation:** Leveraging interpolation and fill-forward/backward logic on a per-vehicle basis to repair the flagged data points, creating a clean, complete dataset ready for analysis.
<img width="500" height="700" alt="image" src="https://github.com/user-attachments/assets/f05876f2-ff00-43a4-9fb5-a71f20aec606" />
<img width="493" height="700" alt="image" src="https://github.com/user-attachments/assets/3cd5f324-d293-4ff7-8d4f-9e391eedbb8b" />


### Phase 1: Residence Identification (DBSCAN)
Focusing on nighttime activity (12 AM - 5 AM), I used the DBSCAN clustering algorithm to identify the densest cluster of each vehicle's location data, designating its centroid as the probable "home residence."
<img width="1272" height="817" alt="image" src="https://github.com/user-attachments/assets/4900680b-2f47-4a68-a790-ffbc492109d5" />

### Phase 2: Charging Location Analysis
A two-pass system was engineered to identify charging events based on positive battery charge deltas. High-confidence locations were identified from significant charge increases (>5%), while a lower threshold was used to find secondary locations for the remaining vehicles.
<img width="500" height="600" alt="image" src="https://github.com/user-attachments/assets/14c19e6e-ff69-4ffb-98c8-4aa2cf45c58b" />
<img width="420" height="600" alt="image" src="https://github.com/user-attachments/assets/9d64d27a-86c9-4968-9d25-42a4fafbff53" />



### Phase 3: Driver Risk Assessment Model
To create a proxy for driver earnings and stability, I engineered a feature for the average daily distance traveled. A Z-score was then calculated for each driver against the fleet average. Drivers with a score below a -1.5 threshold were automatically categorized as "High Risk," providing an early warning system for the risk management team.
<img width="793" height="280" alt="image" src="https://github.com/user-attachments/assets/28750421-904a-47ce-b8b1-4d2c0ff4193f" />

### Phase 4: Business Hotspot Discovery
To prevent bias from parked vehicles, the data was first transformed into a "unique daily visits" log. The DBSCAN algorithm was then applied to this log to discover and map high-traffic commercial zones, defined as areas with over 50 unique vehicle visits within a 500m radius.
<img width="413" height="558" alt="image" src="https://github.com/user-attachments/assets/364f099c-45f3-4335-b232-d4286922291a" />
<img width="520" height="504" alt="image" src="https://github.com/user-attachments/assets/31a2314b-e353-4496-a33f-95d8538bd4f7" />


## 5. Business Impact & Value Delivered

This project successfully translated raw data into tangible business value, providing a significant return on investment.

*   **For the Collections Team:** Delivered a verified dataset of **982 driver residences**, empowering the team with accurate location data to dramatically increase their contact and recovery success rate.
*   **For the Risk Management Team:** The automated risk model proactively identified **29 "High Risk" drivers**, allowing the team to shift from a reactive to a proactive stance, prioritizing intervention to prevent defaults and mitigate financial loss.
*   **For Business Strategy:** The analysis revealed **81 key operational hotspots**, providing the leadership team with data-driven evidence to guide expansion efforts, marketing campaigns, and future charging infrastructure partnerships.

The final deliverable package included a set of automated scripts, final summary CSVs, and a suite of interactive maps for easy consumption by non-technical stakeholders.

<img width="742" height="275" alt="image" src="https://github.com/user-attachments/assets/c673bb99-726d-4fff-93bd-e2e2fc5e7b83" />

*(Example: A key visualization delivered to the client, showing the clear segmentation of High Risk drivers.)*

## 6. Recommended Next Steps for the Client

Upon project completion, I recommended several high-impact next steps to further enhance their data capabilities:
*   **Develop a Predictive Model:** Build a supervised machine learning model (e.g., Logistic Regression) to predict the *probability* of default for more nuanced risk assessment.
*   **Optimize Fleet Operations:** Use the hotspot data to analyze route profitability and suggest optimized routes for drivers.
*   **Integrate External Data:** Enrich the risk model by incorporating external factors like local economic indicators, weather patterns, or traffic data.
