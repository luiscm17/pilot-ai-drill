# Pilot AI Drill - Intelligent Rate of Penetration (ROP) Prediction

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/luiscm17)

## 📋 Project Overview

This project focuses on developing a hybrid machine learning model for predicting Rate of Penetration (ROP) in drilling operations, specifically for geothermal/energy wells. The solution combines mechanistic understanding of drilling physics with advanced machine learning techniques to improve drilling efficiency and reduce operational costs.

## 🎯 Business Problem

Drilling operations account for a significant portion of well construction costs and timelines. Inefficient drilling rates directly impact project economics through:

- Extended rig time
- Increased operational costs
- Delayed revenue generation

Our solution aims to optimize ROP by 15-25% compared to traditional methods, leading to substantial cost savings and improved operational efficiency.

## 🛠️ Technical Stack

- **Core Libraries**:
  - `pandas` - Data manipulation and analysis
  - `numpy` - Numerical computing
  - `scikit-learn` - Machine learning models and utilities
  - `welly` - Well log data handling and visualization
  - `matplotlib` & `seaborn` - Data visualization
  - `jupyter` - Interactive data exploration

- **Development Tools**:
  - `black` - Code formatting
  - `pytest` - Testing framework
  - `pre-commit` - Git hooks for code quality

## 📁 Project Structure

```yml
pilot-ai-drill/
│
├── data/                           # Data storage
│   ├── raw/                       # Raw data (immutable)
│   ├── processed/                 # Processed data
│   └── external/                  # External data sources
│
├── notebooks/                     # Jupyter notebooks
│   ├── 01_eda.ipynb              # Exploratory data analysis
│   ├── 02_feature_engineering.ipynb
│   └── 03_model_development.ipynb
│
├── src/                           # Source code
│   ├── data/                      # Data processing
│   ├── features/                  # Feature engineering
│   ├── models/                    # Model development
│   └── visualization/             # Visualization utilities
│
├── models/                        # Trained models
├── config/                        # Configuration files
├── tests/                         # Unit tests
└── docs/                          # Documentation
```

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- pip (Python package manager)

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/luiscm17/pilot-ai-drill.git
   cd pilot-ai-drill
   ```

2. Create and activate a virtual environment:

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: .\venv\Scripts\activate
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

## 📊 Data

The project uses drilling data from Utah FORGE Well 16-16B(78)-32, including:

- Drilling mechanics (WOB, RPM, Torque)
- Formation characteristics (lithology, mineralogy)
- Environmental conditions (temperature, pressure)
- Gas measurements

## 🤖 Model Development

Our approach combines:

1. **Mechanical Models**: Physical understanding of drilling dynamics
2. **Machine Learning**: Data-driven pattern recognition
3. **Transfer Learning**: Knowledge application across different well conditions

## 📈 Performance Metrics

- **Prediction Accuracy**: MAE < 10 ft/hr
- **Model Performance**: R² > 0.75
- **Error Tolerance**: RMSE < 15 ft/hr

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📬 Contact

For questions or feedback, please contact [luiserwinc@gmail.com](mailto:luiserwinc@gmail.com)

## 🙏 Acknowledgments

- Utah FORGE for providing the drilling data
- Open-source community for the Python data science ecosystem
