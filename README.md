# Egyptian Open-Source Contribution Analysis

Analyzing Egyptian open-source repositories to explore project popularity, contribution patterns, documentation indicators, and differences across programming languages using Python, statistical analysis, and unsupervised learning.

## 📌 Project Overview

Open-source software plays an important role in software development, knowledge sharing, and collaborative innovation. However, understanding the characteristics and popularity of open-source projects within a specific developer community requires data-driven analysis.

This project explores a dataset of GitHub repositories associated with the Egyptian open-source ecosystem. It investigates repository popularity, contributor counts, documentation indicators, and programming language differences.

The project combines **Exploratory Data Analysis (EDA), Statistical Analysis, Hypothesis Testing, and K-Means Clustering** to identify patterns and summarize the characteristics of the collected repositories.

## 🎯 Project Objectives

- Explore the characteristics of Egyptian open-source repositories.
- Investigate the relationship between repository stars, forks, and contributor counts.
- Examine the association between documentation indicators and repository popularity.
- Test whether repository popularity distributions differ across programming languages.
- Segment repositories into groups based on selected numerical characteristics.
- Translate analytical findings into practical recommendations.
- Identify data quality issues and document analytical limitations.

## 📊 Dataset Overview

The dataset was collected from GitHub repositories and contains repository-level and associated GitHub profile information.

The analyzed dataset contains **1,578 repository records and 34 columns** after the initial cleaning step.

### Main Variables

| Category | Variables | Purpose |
|---|---|---|
| Repository Popularity | `stargazers_count`, `forks_count` | Measure repository attention and engagement |
| Contributions | `contribs_count` | Examine contributor counts |
| Repository Activity | `last_repo_commit_date` | Explore repository recency where available |
| Documentation | `documentation_score` | Measure the presence of selected documentation indicators |
| Programming Language | `language` | Compare popularity distributions across languages |
| Issues and Pull Requests | `open_issues`, `closed_issues`, `merged_pull_requests`, and related fields | Explore repository management and collaboration |
| Repository Metadata | `repo_name`, `repo_html_url`, `topics` | Identify and describe repositories |
| Developer Profile | `public_repos`, `followers`, `following`, and related fields | Provide additional context about repository owners |

**Note:** The dataset contains missing values and potential collection limitations. Not every variable was suitable for every analysis.

## 🛠️ Tools and Technologies

- **Python** — Main programming language
- **Pandas** — Data manipulation and analysis
- **NumPy** — Numerical operations
- **Matplotlib / Seaborn** — Data visualization
- **SciPy** — Statistical tests and correlation analysis
- **Scikit-learn** — Feature scaling and K-Means clustering
- **Jupyter Notebook** — Interactive analysis and documentation
- **GitHub** — Repository hosting and project version control

## 🔍 Project Workflow

### 1. Exploratory Data Analysis (EDA)

The initial analysis explored repository characteristics, distributions, missing values, and patterns in the collected dataset.

Key activities included:

- Inspecting dataset structure and data types.
- Examining missing values and data quality.
- Exploring repository popularity and contribution indicators.
- Investigating programming language distributions.
- Visualizing relevant variables and their relationships.

### 2. Statistical Analysis and Hypothesis Testing

Statistical tests were used to investigate relationships and differences within the dataset.

#### Correlation Analysis

Spearman's rank correlation was used to examine monotonic relationships between selected numerical variables.

Key findings:

- **Stars vs. Forks:** A positive association was observed (Spearman's \(\rho = 0.664\), \(p < 0.001\)).
- **Contributors vs. Stars:** No statistically significant association was detected (\(\rho = 0.004\), \(p = 0.876\)).
- **Contributors vs. Forks:** A weak positive association was observed (\(\rho = 0.122\), adjusted \(p < 0.001\)).
- **Documentation Score vs. Stars:** A weak negative association was observed (\(\rho = -0.146\), adjusted \(p < 0.001\)).
- **Documentation Score vs. Forks:** No statistically significant association was detected (\(\rho = -0.025\), \(p = 0.325\)).

Benjamini–Hochberg correction was applied to the relevant multiple correlation tests.

#### Programming Language Comparison

The Kruskal–Wallis test was used to examine differences in repository popularity distributions across programming language groups. Post-hoc pairwise comparisons were conducted using the Mann–Whitney U test with Holm correction.

The omnibus tests indicated statistically significant differences in star and fork distributions across the language groups examined.

Some pairwise comparisons were also statistically significant. For example, PHP repositories had higher median star counts than Dart and C repositories in the significant comparisons, while fork-count differences were observed between PHP and several other language groups.

These results indicate differences in the observed distributions, not that a programming language causes higher popularity.

### 3. Repository Segmentation Using K-Means

K-Means clustering was used to group repositories with similar numerical characteristics.

#### Feature Selection

The final model used:

- `stargazers_count`
- `forks_count`
- `documentation_score`

Stars and forks were transformed using `log1p` to reduce the influence of highly skewed distributions. The selected features were then standardized using `StandardScaler`.

The number of clusters was evaluated using the Elbow Method and Silhouette Score.

#### Sensitivity Analysis

An initial model included `contribs_count`. However, a large proportion of repositories in one cluster had exactly 30 contributors, raising a potential data collection concern.

Contributor counts were excluded from the final model to examine whether the segmentation remained meaningful without this feature. The repeated value of 30 was treated as a potential limitation rather than a confirmed collection cap.

The alternative two-cluster model achieved a Silhouette Score of approximately **0.4596**.

#### Final Cluster Profiles

| Metric | Cluster 0 | Cluster 1 |
|---|---:|---:|
| Repository Count | 1,218 | 360 |
| Percentage | 77.19% | 22.81% |
| Median Stars | 5 | 60.5 |
| Median Forks | 1 | 16 |
| Median Documentation Score | 5 | 5 |

The clusters were interpreted as follows:

- **Cluster 0 — Lower-Popularity Repositories:** Repositories with lower median star and fork counts.
- **Cluster 1 — Higher-Popularity Repositories:** Repositories with higher median star and fork counts.

The clearest distinction between the clusters was repository popularity. Both groups had the same median documentation score, so the clustering results do not establish a difference in median documentation indicators.

The clusters are analytical segments, not definitive categories of repository quality or success.

## 💡 Key Insights

1. **Stars and forks are positively associated.** Repositories with more stars generally tend to have more forks in the analyzed dataset.
2. **Contributor counts alone do not explain popularity.** No significant association was found between contributor counts and stars, while the association with forks was weak.
3. **Documentation indicators do not automatically correspond to popularity.** The documentation score showed a weak negative association with stars and no significant association with forks.
4. **Popularity distributions differ across some programming language groups.** These differences may reflect several factors beyond language choice.
5. **Repositories can be segmented into lower- and higher-popularity groups.** The final clustering model primarily distinguished repositories using stars and forks.
6. **Data quality matters.** Missing values and potential collection limitations influenced feature selection and interpretation.

## 📌 Recommendations

Based on the observed findings:

- **Improve project discoverability:** Use clear repository descriptions, relevant topics, and useful README files to help users understand projects.
- **Encourage meaningful contributions:** Evaluate community engagement using multiple indicators rather than contributor counts alone.
- **Focus on useful documentation:** Prioritize clear installation instructions, usage examples, and contribution guidelines rather than documentation checklist scores alone.
- **Interpret language comparisons carefully:** Consider project purpose, repository age, ecosystem size, and other potential influences before drawing conclusions.
- **Improve data collection:** Ensure repository activity and contributor metrics are collected consistently and investigate potential API or extraction limits.
- **Avoid popularity-only evaluations:** Stars and forks are useful indicators of attention, but they do not fully measure software quality, sustainability, or community impact.

These recommendations are informed by the analysis but were not tested as interventions.

## ⚠️ Limitations

- **Missing data:** Some variables, including last commit dates and repository topics, contain substantial missingness.
- **Potential collection limitations:** The repeated contributor count of 30 may indicate a collection constraint, but this has not been independently verified.
- **Heuristic documentation score:** The score captures selected documentation indicators, not the overall quality or usefulness of documentation.
- **Observational findings:** Statistical associations do not establish causation.
- **Uneven group sizes:** Repository and language groups vary in size, which may affect comparisons.
- **Clustering limitations:** Results depend on the selected features, transformations, scaling, and number of clusters.
- **Dataset scope:** Findings apply to the collected dataset and should not automatically be generalized to all Egyptian developers or open-source repositories.

## 🏁 Conclusion

This project provides an analytical overview of the Egyptian open-source repositories represented in the collected dataset.

By combining EDA, statistical hypothesis testing, and K-Means clustering, the analysis explored repository popularity, contributor counts, documentation indicators, and programming language differences.

The results highlight the relationship between stars and forks, differences in popularity distributions across some programming language groups, and two repository segments characterized primarily by popularity.

The project also demonstrates the importance of validating data quality, choosing features carefully, interpreting statistical significance responsibly, and acknowledging the limitations of observational analysis.


## 🚀 Getting Started

### Prerequisites

- Python 3.10 or a compatible Python version
- Jupyter Notebook or JupyterLab

### Installation

Clone the repository:

```bash
git clone https://github.com/Hazem-Mohammedd/Egyptian-Open-Source-Contribution-Analysis.git
cd Egyptian-Open-Source-Contribution-Analysis
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open the analysis notebook and run the cells in order.

**Note:** Update the paths and dependencies according to the actual repository files and environment.

   
## Acknowledgements

- Special thanks to [GitHub-OpenSource-Analysis](https://github.com/heba14101998/GitHub-OpenSource-Analysis) for conducting the data scraping.

## License
This project is licensed under the MIT License. See the LICENSE file for more information.

---

*This project was developed for analytical and educational purposes using the collected GitHub repository dataset.*
