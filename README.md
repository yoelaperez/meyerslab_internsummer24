ABSTRACT:

Introduction:

The aim of this project is to investigate the cost and benefit of influenza antivirals using disease and health economic models. The objectives are to:
a. Adapt from a cohort study comparing Oseltamivir to Baloxavir
b. Modify our existing antiviral model for household prophylaxis and treatment.
c. Investigate the cost-effectiveness and budget impact analysis: Using (i) basic statistical analysis and (ii) constructing decision trees, transition probabilities, and sensitivity analyses.
d* Cost and Effect Data for two-set of patients: effect data, cost

Methodology:

Based on this study, we want to find out if using baloxavir leads to fewer doctor's visits, hospital stays, and overall healthcare expenses related to complications from the influenza after treatment, compared to oseltamivir.

Summer Internship Summary: (from Yoel Perez-Perez)

Over the past 11 weeks, I have been broadly introduced to infectious disease modeling in the context of health economics research. Despite a slow early start because of on-boarding protocols, the first couple of weeks were devoted to my familiarization with vocabulary and concepts, mainly through reading an article on the economic value of COVID-19 vaccines. In the immediate weeks that followed, I learned to summarize my understanding through creating and presenting slideshows, shared with my mentor but accessible to a non-technical audience. While I also learned the basic ideas of compartmental epidemiology models, I programmed my first simulations in Python, using my pre-existing knowledge of numpy, scipy, pandas, and matplotlib. Soon, I was tasked with identifying and narrowing our source of publications for a project on the cost-effectiveness of Influenza antivirals. My assigned readings focused on Oseltamivir Phosphate and Baloxavir Marboxil, and because my mentor encouraged exploration, I quickly became exposed to the world of clinical trials and FDA documentation. Cost-effectiveness analysis is a dense subfield of health economics, which required me to read brief excerpts from a textbook to better grasp the critical metrics and formulas. Our project question was as follows: if Baloxavir Marboxil is an antiviral that requires fewer doses than Oseltamivir Phosphate to reduce the illness and transmissibility caused by Influenza, could it be more cost-effective to employ in an epidemic setting despite its higher cost per dose? The presumptive hypothesis was that Baloxavir is more cost-effective than Oseltamivir. To test this idea, I was tasked with writing programs that processed clinical Influenza data from patients taking either antiviral (as well as a control of no treatment), computed economic metrics for cost-effectiveness, and then visualized the economic value of the treatments relative to each other and a control. Because of its versatility for statistical analysis of data, modeling, and visualization, I learned the basics of the R language and employed it for the remainder of the project. Most data used was in .csv file format, obtained from academic publications and government sources. Over several weeks of Zoom meetings and technical guidance from my mentor, I produced four iterations of R programs, resulting in a total of around 6 separate code scripts, each with a few hundred lines. This required me to keep a detailed commenting system in place while also translating my programming into scientific protocols. Our work soon intersected with the world of health policy in the United States, as some of our methodology drew from COVID-19 evaluations and real CDC-documented Influenza seasons in the United States prior to the COVID-19 pandemic. After generating over 18 almost publishable graphs and tables, my programming and interpretation of the inputted clinical data ultimately suggested that after 30 days of patient observation, Oseltamivir may be most cost-effective, contrary to our original hypothesis. Although our summer research has come to an end, I would have liked to more rigorously test my results and our hypothesis through probabilistic analysis and other statistical methods, as well as eventually incorporating recent local clinical data from Austin Influenza patients. Once tested, such work could be combined with a compartmental model to form a more realistic simulation of Influenza antiviral health economics, deployable for future seasons or outbreaks because of its foundation in real clinical data. I hope to publish my programs on GitHub and share my experience soon while potentially attending infectious disease modeling conferences in the fall. This summer, I have learned to teach myself technical concepts by reading academic literature and discussing methodology alongside results. I have also grown in my skill set for scientific inquiry, expanded my arsenal as a programmer, and matured in my ability to use and interpret real-world datasets. I remain deeply grateful to Oluwasegun for his mentorship and equally in awe of the opportunities offered by the Meyers Lab.

Method in Clinical Study: 

Patients who got a prescription for either baloxavir or oseltamivir within 48 hours after visiting a doctor for the influenza during the 2018-2019 influenza season were studied. They used a database to find these patients and made sure the groups were similar by matching two people who took oseltamivir with one person who took baloxavir. They then checked on these patients 15 and 30 days after they started the antiviral treatment to see how much healthcare they needed and how much it cost, focusing on any cause, any breathing-related issues, and specific conditions like the influenza, asthma, COPD, or infections. 

Method in Modeling Study: 

The following initial sequence is the same between the two cost-effectiveness analysis programs written in R:

The R library “tidyverse” is imported for greater functionality, including visualization and syntactic tools. The document options are adjusted to turn-off scientific notation, to better view large numbers.
Three simulated populations (“samplesizeA”, “samplesizeB”, and “samplesizeC”**) were stored as numeric variables, corresponding to Treatment A (Baloxavir Marboxil) and Treatment B (Oseltamivir Phosphate) and Treatment C (No Treatment, Control). All population sizes were totalled as a sum “totalss” (numeric). Group A is assumed to have better clinical outcomes.
“samplesizeA” is of size 5000; “samplesizeB” is of size 10000; “samplesizeC” is of size 10000. This is intended to approximate the propensity match (1 Bal. : 2 Osel.) performed by Neuberger et. al.
“samplesizeC” is of identical size to Treatment Group B (1:1 Propensity Match) is created to act as the control of no treatment.
A dataframe is created as “simdataset”, containing the indexing column “serial”, or a vector of numbers from 1 to “totalss”. (This column is relabeled as “id”.)
A column “group” is added to the dataframe, creating Groups A, B, and C (grouped top to bottom) as factors with sample sizes from the numeric variables above.
A column “trtcourse_cost” is added to the dataframe, representing the initial fixed cost of either antiviral treatment, where Treatment A is $170.49 and Treatment B is $50.00, according to collected pharmacy data (see Excel document).
Group C will have no initial cost, or an initial fixed cost of $0.00
**Group C cost data is obtained from Peters et. al., where 2005 USD is converted to 2019 USD using the following equation (from State of California): 2019 Cost = 2005 Cost * (2019 CPI / 2005 CPI)
(2019 CPI / 2005 CPI) = (549.077/328.4) = 1.672
The following factor was applied to the following 2005 cost data (Peters): “Inpatient acute”, “ER visits”, “Total outpatient”, “Outpatient pharmacy”.
Calculation data used is from BLS Consumer Price Index Archived News Releases (Dec 2019 and Dec 2005), values are both the “unadjusted indexes” under the entry “medical care” or “medical care services”.
**Group C HCRU data comes from Putri et. al. utilizing the following categories: “Hospitalizations”, “Emergency Department…”, “Outpatient visits”, “Ill but not…”
The number of events overall by category was divided by the total number of events overall (done for each category).  This functions analogously to the frequency of HCRU events occurring. At the present, no SD was computed.

At this point, two R programs differ in data. Program 1 contains the 15-day outcomes while Program 2 contains the 30-day outcomes from Neuberger et. al. Both programs use the exact same no-treatment (Group C) data as the analysis baseline. The following structure is identical between the two R programs, except for the input data:

Four pairs of matching data columns are added to the dataframe “simdataset”. Each pair of columns corresponds to first the “event frequency” of healthcare resource utilization (HCRU) followed by the cost of each HCRU event, as extracted from the appendix in Neuberger et. al. NOTE: Study data used corresponds to the “all-cause” data in appendix tables; in particular, the “mean number” rows are the input data, which is measured as a ratio of the total occurrences per total patients in the sample of treatment. The four pairs of event/cost data include the following categories:
ER visits (“er_event”/“er_cost”)
Hospitalization (“hosp_event”/“hosp_cost”)
Outpatient visits (“outpt_event”/“outpt_cost”)
Prescriptions (“pres_event”/“pres_cost”)
A summary of the categorical HCRU events per patient (each row entry) are added together into a column named “total_events”.
A column “totalcost” is added to the dataframe as a sum of “trtcourse_cost” and all “_cost” columns above. Total values correspond to each patient (each row entry).
A column “totalutility” is added to the dataframe as a sum of multiples of the “_event” columns above. Total values correspond to each patient (each row entry). Each “_event” column is multiplied by a certain utility (fraction of 1). Utility values are approximated as those corresponding to different disease states (obtained from Padula et. al.) which most align with the event from Neuberger et. al. Utilities are assigned and computed as follows:
U(Infectious_2) = 0.500 → er_event * 0.500 
U(Infectious_3) = 0.250 → hosp_event * 0.250
U(Infectious) = 0.833 → outpt_event * 0.833
U(Exposed) = 0.880 → pres_event * 0.880
In order to compute QALY values for utility:
Equations a, c, and d were multiplied by (7/365) → the median days of illness for outpatients
Equation b was multiplied by (21/365) → the median days of illness for inpatients
Dataframes are created from “simdataset” filtering data by Treatment Group (named: “Group A”, “Group B”, “Group C”)
A dataframe “deltatab” is created to effectively store ICER calculations (separated by cost and utility), containing the following columns: (“BL” = Baseline)
“deltaCost_A”, computed as “GroupA$totalcost - “GroupC$totalcost”, BL = no treatment
“deltaUtil_A”, computed as “GroupA$totalutility - “GroupC$totalutility”, BL = no treatment
“deltaCost_B”, computed as “GroupB$totalcost - “GroupC$totalcost”, BL = no treatment
“deltaUtil_B”, computed as “GroupB$totalutility - “GroupC$totalutility”, BL = no treatment
“deltaCost_trt”, computed as “GroupA$totalcost - “GroupB$totalcost”, BL = Oseltamivir
“deltaUtil_trt”, computed as “GroupA$totalutility - “GroupB$totalutility”, BL = Oseltamivir
All remaining code is primarily aesthetic to produce the following types of visualizations:
A Cost-Effect Plane, plotting the C data vs. E data per treatment as computed above. 
Various willingness-to-pay lines originating at $0/[Unit Effect] are drawn and color-coded to show increasing WTP thresholds (ranging from $10,000 to $700,000 per QALY) and to compare how many simulations are “cost-effective” by remaining under the line in the cost domain.
The above determination is executed with a loop algorithm that also outputs the ratio of points that are cost-effective out of 10000, or “samplesizeC”. This algorithm is used for the next visualization.
A Cost-Effectiveness Acceptability Curve (CEAC), plotting the percent of points that are cost-effective at each of the given WTP values.
A scatter plot visualizing how total cost varies against the total HCRU (“simdataset$total_events”), separated by Treatment (A and B).

REFERENCES:

Du, Z., Nugent, C., Galvani, A. P., Krug, R. M., & Meyers, L. A. (2020). Modeling mitigation of influenza epidemics by baloxavir. Nature communications, 11(1), 2750. https://doi.org/10.1038/s41467-020-16585-y

Nagase, H., Moriwaki, K., Kamae, M., Yanagisawa, S., & Kamae, I. (2009). Cost-effectiveness analysis of oseltamivir for influenza treatment considering the virus emerging resistant to the drug in Japan. Value in health : the journal of the International Society for Pharmacoeconomics and Outcomes Research, 12 Suppl 3, S62–S65. https://doi.org/10.1111/j.1524-4733.2009.00629.x

Padula, W. V., Malaviya, S., Reid, N. M., Cohen, B. G., Chingcuanco, F., Ballreich, J., … Alexander, G. C. (2021). Economic value of vaccines to address the COVID-19 pandemic: a U.S. cost-effectiveness and budget impact analysis. Journal of Medical Economics, 24(1), 1060–1069. https://doi.org/10.1080/13696998.2021.1965732

Newall AT, Wood JG, Oudin N, MacIntyre CR. Cost-effectiveness of pharmaceutical-based pandemic influenza mitigation strategies. Emerg Infect Dis. 2010 Feb;16(2):224-30. doi: 10.3201/eid1602.090571. PMID: 20113551; PMCID: PMC2957998.

Stat Pharm. (2018, September 16). Probabilistic Sensitivity Analysis for Health
Economic Evaluation using R. https://www.youtube.com/watch?v=b7v5xIigcn4

Venkatesan, S., Myles, P. R., Bolton, K. J., Muthuri, S. G., Al Khuwaitir, T., Anovadiya, A. P., Azziz-Baumgartner, E., Bajjou, T., Bassetti, M., Beovic, B., Bertisch, B., Bonmarin, I., Booy, R., Borja-Aburto, V. H., Burgmann, H., Cao, B., Carratala, J., Chinbayar, T., Cilloniz, C., … Nguyen-Van-Tam, J. S. (2019). Neuraminidase Inhibitors and Hospital Length of Stay: A Meta-analysis of Individual Participant Data to Determine Treatment Effectiveness Among Patients Hospitalized With Nonfatal 2009 Pandemic Influenza A(H1N1) Virus Infection. The Journal of Infectious Diseases, jiz152. https://doi.org/10.1093/infdis/jiz152

Stat Pharm. (2020, February 14). PSA using R: Hands-on tutorial. https://www.youtube.com/watch?v=Z_Q_3de9zJ4

Komeda, T., Takazono, T., Hosogaya, N., Miyazaki, T., Ogura, E., Iwata, S., Miyauchi, H., Honda, K., Fujiwara, M., Ajisawa, Y., Watanabe, H., Kitanishi, Y., Hara, K., & Mukae, H. (2021). Comparison of Hospitalization Incidence in Influenza Outpatients Treated With Baloxavir Marboxil or Neuraminidase Inhibitors: A Health Insurance Claims Database Study. Clinical infectious diseases : an official publication of the Infectious Diseases Society of America, 73(5), e1181–e1190. https://doi.org/10.1093/cid/ciaa1870

Campbell, A. P., Tokars, J. I., Reynolds, S., Garg, S., Kirley, P. D., Miller, L., Yousey-Hindes, K., Anderson, E. J., Oni, O., Monroe, M., Kim, S., Lynfield, R., Smelser, C., Muse, A. T., Felsen, C., Billing, L. M., Thomas, A., Mermel, E., Lindegren, M. L., … Fry, A. M. (2021). Influenza Antiviral Treatment and Length of Stay. Pediatrics, 148(4), e2021050417. https://doi.org/10.1542/peds.2021-050417

Neuberger, E., Wallick, C., Chawla, D., & Castro, R. C. (2022). Baloxavir vs oseltamivir: reduced utilization and costs in influenza. The American journal of managed care, 28(3), e88–e95. https://doi.org/10.37765/ajmc.2022.88786

How to Use the Consumer Price Index (CPI). (n.d.). State of California: Department of Finance. https://dof.ca.gov/wp-content/uploads/sites/352/Forecasting/Economics/Documents/How-To-Use-CPI-Data.pdf

Peters, P. H., Moscona, A., Schulman, K. L., & Barr, C. E. (2008). Study of the impact of oseltamivir on the risk for pneumonia and other outcomes of influenza, 2000-2005. Medscape journal of medicine, 10(6), 131.

Consumer Price Index Archived News Releases. (n.d.). Bureau of Labor Statistics. Retrieved August 9, 2024, from https://www.bls.gov/bls/news-release/cpi.htm

Putri, W. C. W. S., Muscatello, D. J., Stockwell, M. S., & Newall, A. T. (2018). Economic burden of seasonal influenza in the United States. Vaccine, 36(27), 3960–3966. https://doi.org/10.1016/j.vaccine.2018.05.057

Wan, X., Wang, W., Liu, J., & Tong, T. (2014). Estimating the sample mean and standard deviation from the sample size, median, range and/or interquartile range. BMC Medical Research Methodology, 14(1), 135. https://doi.org/10.1186/1471-2288-14-135

Hollmann, M., Garin, O., Galante, M., Ferrer, M., Dominguez, A., & Alonso, J. (2013). Impact of influenza on health-related quality of life among confirmed (H1N1) 2009 patients. PloS one, 8(3), e60477.


SOURCES FOR FLU SEASON DATA:

National, Regional, and State Level Outpatient Illness and Viral Surveillance. (n.d.). Retrieved August 15, 2024, from https://gis.cdc.gov/grasp/fluview/fluportaldashboard.html

Laboratory-Confirmed Influenza Hospitalizations. (n.d.). Retrieved August 15, 2024, from https://gis.cdc.gov/grasp/fluview/FluHospRates.html
