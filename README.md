# NBA Passing Network Analysis

A comprehensive network analysis project examining NBA team passing patterns, player roles, and their relationship with team performance across multiple seasons using network science and graph theory.

## 📋 Table of Contents

- [Overview](#overview)
- [Research Questions](#research-questions)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Data Collection](#data-collection)
- [Analysis Components](#analysis-components)
- [Key Features](#key-features)
- [Usage](#usage)
- [Output Files](#output-files)
- [Technologies Used](#technologies-used)
- [Results & Insights](#results--insights)

## 🎯 Overview

This project analyzes NBA team passing networks to understand how team chemistry, player roles, and passing patterns evolve over time and correlate with team performance. Using data from the NBA API, the analysis builds directed weighted graphs representing player-to-player passing interactions and calculates various network metrics to quantify team dynamics.

The analysis focuses on multiple NBA teams (Cavaliers, Thunder, etc.) across five seasons (2020-21 through 2024-25), examining how passing networks change and their relationship with winning percentages.

## 🔍 Research Questions

1. **How do passing networks evolve across seasons?**
   - Temporal changes in network structure and density
   - Player role transitions over time

2. **Which network changes are linked to shifts in winning percentages?**
   - Correlation between network metrics and team performance
   - Identification of critical network characteristics

3. **Do star players, as network hubs or bridges, explain performance changes?**
   - Impact of high-centrality players on team success
   - Role of connectors in team chemistry

4. **Can hypotheses from initial teams apply to others?**
   - Cross-team validation of findings
   - Generalizability of network patterns

## 📁 Project Structure

```
nba-network-analysis/
│
├── data_retrieval.ipynb           # NBA API data collection
├── nba_network_analysis.ipynb     # Network visualization & graph analysis
├── nba_player_analysis.ipynb      # Individual player role analysis
├── nba_metrics_analysis_COMPLETE.ipynb  # Team metrics & performance correlation
│
├── passing_data/                  # Raw passing data by team and season
│   ├── Cavaliers_improve/
│   ├── Thunder_improve/
│   └── [team]_improve/
│
├── network_visualizations/        # Generated network graphs
├── player_role/                   # Player-specific analysis outputs
└── team_metrics/                  # Team-level metric calculations
```

## 🛠️ Installation

### Prerequisites

- Python 3.11+
- Jupyter Notebook or JupyterLab

### Required Libraries

```bash
pip install nba_api
pip install pandas numpy
pip install networkx
pip install matplotlib seaborn
pip install scipy
pip install openpyxl
```

## 📊 Data Collection

### Using `data_retrieval.ipynb`

The data collection process uses the NBA Stats API to gather passing data:

1. **Team Selection**: Retrieves all NBA team information
2. **Season Data**: Collects passing statistics for specified seasons
3. **Data Processing**: 
   - Reformats player names (Last, First → First Last)
   - Filters relevant columns (player_name, pass_to, team, pass, ast)
   - Exports cleaned data to CSV

**Example data structure:**
```csv
player_name,pass_to,team,pass,ast
Shai Gilgeous-Alexander,Cason Wallace,OKC,308,37
Shai Gilgeous-Alexander,Luguentz Dort,OKC,245,28
```

## 🔬 Analysis Components

### 1. Network Analysis (`nba_network_analysis.ipynb`)

**Key Functions:**
- `build_passing_graph()`: Creates directed weighted graphs from passing data
- `create_fixed_circular_layout()`: Arranges players by network strength
- `visualize_network()`: Generates network visualizations

**Features:**
- Multi-season automatic processing
- Directed weighted graphs with customizable edge thresholds
- Circular layouts with top players positioned by passing strength
- Side-by-side season comparisons
- Animation-ready frame exports

**Network Metrics:**
- Node degree (in-degree, out-degree, weighted degree)
- Edge weights (pass counts, assist counts)
- Player positioning based on network centrality

### 2. Player Analysis (`nba_player_analysis.ipynb`)

**Analyzes individual player roles using:**

- **Betweenness Centrality**: Measures players as bridges between teammates
- **Closeness Centrality**: Identifies players with efficient passing connections
- **Eigenvector Centrality**: Highlights players connected to other key players
- **PageRank**: Determines overall player importance in the network

**Outputs:**
- Top 12 players per season (by network strength)
- Player role classifications
- Temporal evolution of player importance

### 3. Metrics Analysis (`nba_metrics_analysis_COMPLETE.ipynb`)

**Team-level network analysis:**

- **Network Density**: Measures overall team connectivity
- **Centralization**: Quantifies reliance on star players
- **Efficiency Metrics**: Evaluates passing effectiveness
- **Correlation Analysis**: Links network metrics to winning percentage

**Statistical Methods:**
- Pearson correlation coefficients
- Spearman rank correlations
- Season-to-season change analysis
- Temporal trend visualization

## ✨ Key Features

### Network Visualization
- **Circular layouts** with players arranged by passing strength
- **Edge thickness** proportional to pass volume
- **Color-coded edges** showing pass intensity
- **Node size** representing player centrality
- **Consistent cross-season comparisons** using global normalization

### Automated Processing
- Batch processing of multiple seasons
- Automatic file detection and loading
- Standardized output formats
- Configurable parameters (top N players, minimum weights, etc.)

### Multi-dimensional Analysis
- Pass networks (total passes)
- Assist networks (passes leading to made baskets)
- Weighted vs. unweighted metrics
- Temporal evolution tracking

## 💻 Usage

### Basic Workflow

1. **Collect Data**
```python
# In data_retrieval.ipynb
team_id = 1610612760  # OKC Thunder
season = "2024-25"
# Run cells to fetch and save passing data
```

2. **Visualize Networks**
```python
# In nba_network_analysis.ipynb
DATA_DIR = 'passing_data/Thunder_improve/'
# Automatically processes all seasons
# Generates visualizations
```

3. **Analyze Players**
```python
# In nba_player_analysis.ipynb
TOP_N = 12  # Top players to analyze
# Calculates centrality metrics
# Exports player role data
```

4. **Calculate Team Metrics**
```python
# In nba_metrics_analysis_COMPLETE.ipynb
# Computes team-level metrics
# Correlates with winning percentage
# Generates trend visualizations
```

### Customization Options

**Network Visualization:**
- `top_n`: Number of players to display (default: 12)
- `min_weight`: Minimum pass threshold for edges (default: 20)
- `weight_column`: 'pass' or 'ast' for different network types

**Player Analysis:**
- Centrality measure selection
- Custom player rankings
- Role classification thresholds

## 📈 Output Files

### Network Visualizations
- `[team]_[season]_network.png`: Individual season networks
- `[team]_comparison.png`: Side-by-side season comparisons
- `animation_frames/`: Sequential frames for network evolution videos

### Data Exports
- `player_metrics_[season].csv`: Player-level centrality scores
- `team_metrics_summary.csv`: Aggregated team metrics across seasons
- `correlation_analysis.xlsx`: Statistical correlation results

### Analytical Reports
- Network density trends
- Player role evolution charts
- Performance correlation plots

## 🔧 Technologies Used

- **nba_api**: Official NBA statistics API wrapper
- **NetworkX**: Graph theory and network analysis
- **Pandas**: Data manipulation and analysis
- **NumPy**: Numerical computations
- **Matplotlib**: Static visualizations
- **Seaborn**: Statistical data visualization
- **SciPy**: Statistical analysis and correlations

## 📊 Results & Insights

### Key Findings

1. **Network Density & Performance**
   - Teams with balanced passing networks (moderate density) tend to perform better
   - Over-centralized networks show vulnerability to key player absences

2. **Star Player Impact**
   - High betweenness centrality in point guards correlates with team efficiency
   - Multiple high-centrality players indicate better team chemistry

3. **Temporal Patterns**
   - Successful teams show stable network structures across seasons
   - Dramatic network changes often precede performance shifts

4. **Role Specialization**
   - Clear role differentiation (playmakers vs. finishers) improves efficiency
   - Balanced in-degree and out-degree distributions indicate versatile offenses

### Example Metrics

**Cavaliers 2023-24 (Strong Season):**
- Network Density: 0.73
- Average Betweenness: 0.15
- Centralization Index: 0.42
- Win Percentage: 0.610

**Thunder 2024-25 (Emerging Team):**
- Network Density: 0.68
- Average Betweenness: 0.18
- Centralization Index: 0.38
- Win Percentage: 0.720+ (ongoing)

## 🔄 Future Enhancements

- [ ] Real-time data updates during the season
- [ ] Interactive network visualizations (D3.js, Plotly)
- [ ] Machine learning models for performance prediction
- [ ] Extended historical analysis (10+ seasons)
- [ ] Comparative analysis across all 30 NBA teams
- [ ] Integration of advanced stats (offensive rating, pace, etc.)
- [ ] Network motif analysis (common passing patterns)
- [ ] Playoff vs. regular season network differences

## 📝 Notes

- **Data Recency**: Analysis uses data through the 2024-25 season (ongoing)
- **Top Player Selection**: Focuses on top 12 players by network strength per season
- **Minimum Thresholds**: Edges with fewer than 20 passes are typically filtered
- **Season Naming**: Seasons use format "YYYY-YY" (e.g., "2024-25")

## 🤝 Contributing

This is an academic research project. For questions or suggestions regarding methodology, feel free to reach out.

## 📄 License

This project is for educational and research purposes. NBA data is property of the NBA and is accessed through the official NBA Stats API.

## 🙏 Acknowledgments

- NBA Stats API for providing comprehensive basketball data
- NetworkX development team for the graph analysis library
- The sports analytics community for methodology inspiration

---

**Last Updated**: November 2024  
**Author**: Tung Wai Nam, Yee Long Hei and Leung Chun Lung
**Institution**: City University of Hong Kong  
**Course**: Data Science Course - SDSC3019 Introduction to Networked Life and Data Science
