# Social Network Analysis Application in HR Analytics

![Image](https://github.com/user-attachments/assets/8a97e252-641f-4d0e-9c1e-ca0cefa2e4a5)

## Project Background
This HR project starts from my first assignment for the social network analysis utilizing node-edge structures in the **6303 course**. To further understand and develop my analytical skills, I found a big data set from an open source—the **Enron data set**—which contains over 0.5 million emails.

From there, I tried to explore how organizational structure and communication risk can be diagnosed using **network analysis**, based on email data from Enron executives and key personnel. Since it is a large scale, I tried to scratch the surface of the organization and dive deeper into the individual level. The goal of this project is to translate large-scale, unstructured communication data into practical insights that can support organizational risk diagnosis from an HR analytics perspective.

The dataset consists of approximately **500,000 email messages exchanged among about 150 Enron users**, primarily senior management. The data was collected and prepared by the CALO Project and released publicly during the FERC investigation. Given the scale and unstructured nature of the data, the primary objective was to build an analytical pipeline that balances solid methods with practical interpretability.
*(More details: https://www.cs.cmu.edu/~enron/)*

## Data Preparation and Response Behavior
The raw data was messy. To improve signal quality, system-generated emails such as **auto-replies, newsletters, spam, and calendar notifications** were excluded, as they do not represent meaningful work-related interaction.

I also applied a logic called **Content Value Check**. Very short messages (under 30 characters) were filtered out to avoid overstating connectivity based on low-information exchanges like simple "Thanks" or "OK." This filtering process refined the initial 500,000 messages down to approximately **327,000 valid interactions**, ensuring high analytical precision.

Because response behavior is a central indicator in this project, **response time (RT)** was defined conservatively as the elapsed time between an initial email and the recipient’s first confirmed reply. Simply receiving a message was not treated as evidence of responsiveness; only observed reply behavior was used to measure communication delay and processing speed.

## Network Construction
Email interactions were modeled as a directed, weighted network in which **nodes** represent individuals and **edges** represent communication flows. While the underlying data is individual-level, the analysis intentionally moves beyond individual behavior to examine structural patterns.

I grouped individuals into functional communication units (Communities) centered around key leaders. This allowed the analysis to approximate **de facto organizational structures** that emerge from actual communication patterns rather than relying on formal org charts. This approach reflects how work often flows in practice, especially in complex organizations.

## Key Network Metrics
Several network-based indicators were used to interpret organizational dynamics:

* **Openness (E-I Index)**: This metric is widely applied in ONA (Organizational Network Analysis) to find silos in the organization. It compares internal versus external communication volumes within each unit.
* **Response Time (RT)**: Used as a proxy for organizational sluggishness. **24 hours** was treated as a practical threshold beyond which communication delay may indicate bottlenecks or process friction.
* **Fragmentation Impact**: Estimates structural importance by calculating the percentage loss of overall network connectivity when a given unit is removed.

Together, these indicators are used to address a core HR question:

***Which parts of the organization quietly hold everything together, and which parts introduce risk by being too closed, too slow, or too overloaded?***

## Organizational Network Diagnostics (Macro View)
<img width="1200" height="800" alt="Image" src="https://github.com/user-attachments/assets/528211d4-d075-473b-9dc8-c4f7be48dff6" />
At the macro level, the analysis suggests that Enron’s communication network relied heavily on a small number of very large organizational units that exhibited both inward-facing communication patterns and slow response times.

* **Bureaucratic Silo**: As seen in the chart, groups like **Richard Shapiro’s** and **Tana Jones’s** are massive but extremely closed (Low Openness). They act as bottlenecks with slow response times (50+ hours).
* **High Dependency**: These units showed high **fragmentation impact (over 30%)**, meaning that if they were removed or became inactive, a substantial portion of the overall network would disconnect.

From a practical HR perspective, this combination points to structural vulnerability: core units that are essential for connectivity, yet insulated from cross-functional visibility and feedback.

In contrast, the analysis identified a single unit (**Vince Kaminski’s group**) that functioned as the primary bridge between otherwise siloed parts of the organization. While this unit showed relatively open communication patterns, its response times exceeded the 24-hour threshold, suggesting **overload rather than inefficiency**. This reflects a common organizational risk pattern in which external communication responsibilities accumulate in one place as other units retreat inward, increasing the likelihood of burnout and system-level failure.


## Individual-Level Signals (Micro View)
<img width="1000" height="700" alt="Image" src="https://github.com/user-attachments/assets/274d553e-bea7-455f-9479-fe5fb5a28ded" />
'Simulation Stress Test' to quantify the impact of specific individuals on network stability.  This analysis successfully identified key **"Connectors"** such as **Kenneth Lay, Jeff Skilling, and Shelley Corman**. As shown in the plot, these individuals hold high structural influence (high Y-axis values) despite varying levels of email volume. The fact that the model blindly identified the company's top executives as structural hubs validaties the accuracy of the network metrics.

The simulation results further confirmed their importance: removing the top 10 Connectors caused a **4.16% loss** in network connectivity, whereas removing the top 10 high-volume users (Load Absorbers) resulted in only a **0.89% loss**. This **4.7x difference** proves that organizational continuity is maintained not by official workload, but by a handful of key talents who structurally hold the network together.

The results revealed that organizational continuity hangs by a thread, dependent on a specific few. In Richard Shapiro’s unit, identified as a 'Bureaucratic Silo' in the macro analysis, removing the top 10 Load Absorbers resulted in a negligible network connectivity loss of 0.89%. However, removing the **top 10 Connectors caused the loss to spike to 4.16%—a nearly 4.7x(($4.16 \div 0.89 \approx 4.67) difference.** This disparity was even more extreme in Vince Kaminski’s 'Overloaded Hub,' where the loss from removing **Connectors (2.94%) was nearly 8 times greater than removing Load Absorbers (0.37%)**. This proves that network stability is not maintained by those with official titles or high workloads, but by a handful of 'Hidden Key Talents' who structurally hold the organization together.

## Limitations & Future Considerations
While this project revealed deep insights, there are limitations to consider for future application:

1.  **Context Limitations (Email ≠ Work)**: This analysis uses email metadata. It does not capture face-to-face meetings, calls, or the *sentiment* of the messages (e.g., whether a delay was due to deep work or neglect).
2.  **Snapshot vs. Trend**: The current analysis looks at the data as a whole. A time-series analysis would be better to see how bottlenecks form during specific crisis periods.

## Why This Matters for HR Leaders
This project demonstrates how communication network patterns can serve as **early indicators of organizational risk** before they manifest as turnover or failed projects. The macro analysis identified systemic vulnerabilities like the opacity of 'Bureaucratic Silo' and the burnout risks of 'Overloaded Hubs,' while the micro simulation revealed that these fragile structures are often sustained by a small group of critical Connectors.

Traditional HR metrics often capture outcomes too late. HR leaders need to shift from evaluating individuals to diagnosing the system itself. The true value of analytics lies in identifying exactly who is piercing the opacity of a closed unit and who is preventing the collapse of an overloaded one. 

For HR leaders, the value of this approach lies not in labeling individuals, but in diagnosing systems. **Network-based analytics can support more informed decisions around organizational design, workload distribution, leadership pipelines, and risk governance, helping HR shift from reactive reporting to proactive organizational sensing**.

---

## Metrics Dictionary

| Metric / Term | Definition | How It’s Calculated | HR Interpretation |
|:---|:---|:---|:---|
| **Response Time (RT)** | Average time taken to reply to an email | Time difference between an initial message and the first confirmed reply | Proxy for decision speed and workflow friction |
| **24-Hour Threshold** | Practical risk cutoff for response delay | RT > 24 hours | Indicates potential bottlenecks or overload |
| **E–I Index (Openness)** | Balance of internal vs. external communication | (External − Internal) / (External + Internal) | Values near −1 suggest silos (closed groups) |
| **Frag Impact %** | Structural importance of a unit | % loss of total network connectivity if the unit is removed | Indicates backbone dependency ("Too big to fail") |
| **LCC Loss %** | Simulation shock score (Turnover Risk) | % reduction in the Largest Connected Component after removing specific nodes | Measures how much the network breaks when key talent leaves |
| **Black Hole** | **Typology:** Large, closed, and slow unit | EI < -0.5 and RT > 50h | High risk of opacity, information hoarding, and silos |
| **Overloaded Hub** | **Typology:** Open but overwhelmed unit | EI > -0.2 but RT > 50h | Bottleneck caused by capacity limits, high burnout risk |
| **Bureaucratic** | **Typology:** Small, isolated, internal-focused | EI ≈ -1 and Low connectivity | Disconnected from company goals, process-heavy |
| **Upward Comm Ratio** | Degree of communication directed upward | Messages to executives vs. lateral peers | May signal process bypass or reporting bias |

---

## Appendix: Raw Analysis Log

The following terminal output demonstrates the actual execution of the analysis pipeline. It highlights the identification of "Black Hole" (Richard Shapiro, Tana Jones) and "Overloaded Hub" (Vince Kaminski) organizations, along with the results of the micro-simulation stress tests.
```text
[Enron HR Analytics] Network-based Bottleneck & Role Diagnostics (Final)
[System] ETL Start (Limit: 500,000)
500,000 lines | kept: 327,448
[ETL Done] kept rows: 327,448 
[Network] Nodes: 19,441 | Edges: 185,531
[Macro] Detecting Communities & Calculating Metrics...
[Macro] Modularity(Q): 0.3810 (Community Quality Index)

**[Top10 Macro] Top Organizations by Frag Impact**
                      Dept_ID  Size  Frag_Impact_%  EI_Index  Avg_Response_H  Typology
           C1_richard.shapiro  6570          34.01     -0.59           54.46  🔴 Black Hole
                C2_tana.jones  5951          30.83     -0.64           53.24  🔴 Black Hole
            C3_vince.kaminski  4284          22.10     -0.15           50.22  🟠 Overloaded Hub
                C4_lisa.brown   796           4.11      0.42           47.95  🟠 Overloaded Hub
             C5_michelle.cash   689           3.55      0.23           35.34  🟠 Overloaded Hub
         C6_colette.weinreich   374           1.93      0.40           74.85  🟠 Overloaded Hub
             C7_all.worldwide   279           1.44     -0.49            0.50  🟡 Bureaucratic
               C8_mark.fisher   180           0.93     -0.91           33.93  🔴 Black Hole

**[Micro Simulation] Bottleneck Org Top10 Stress Test (Remove Top10 Individuals)**
Dept: C1_richard.shapiro | Typology=🔴 Black Hole | Frag=34.01% | EI=-0.59
   [Remove Load Absorber Top10] LCC Loss% = 0.89
   [Remove Connector Top10]     LCC Loss% = 4.1
Dept: C2_tana.jones | Typology=🔴 Black Hole | Frag=30.83% | EI=-0.64
   [Remove Load Absorber Top10] LCC Loss% = 1.18
   [Remove Connector Top10]     LCC Loss% = 1.85
Dept: C3_vince.kaminski | Typology=🟠 Overloaded Hub | Frag=22.1% | EI=-0.15
   [Remove Load Absorber Top10] LCC Loss% = 0.37
   [Remove Connector Top10]     LCC Loss% = 2.94
