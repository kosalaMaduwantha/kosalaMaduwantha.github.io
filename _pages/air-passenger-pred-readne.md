---
title: "Air Passenger Readme"
permalink: /air-passenger-pred-readme/
layout: single
classes: wide
# author_profile: true
---

# Air Passenger Satisfaction Dashboard 🛫

A comprehensive web-based data visualization and analytics dashboard for analyzing airline passenger satisfaction metrics using machine learning and interactive data visualizations. This project combines predictive analytics with real-time interactive visualizations to provide insights into passenger satisfaction patterns.

## 📋 Project Overview

This application is an end-to-end data science project that performs passenger satisfaction prediction and analysis using machine learning models. The dashboard provides interactive visualizations for exploring satisfaction patterns across multiple dimensions:

### Key Features
- **Interactive Data Visualizations**: Real-time, responsive charts and graphs built with Plotly
- **Multi-dimensional Analysis**: Explore satisfaction across various passenger attributes
- **Responsive Design**: Mobile-friendly interface using Bootstrap components
- **Classification Analytics**: Deep dive into categorical passenger data
- **Service Rating Analysis**: Comprehensive view of 9 different service categories
- **Predictive Modeling**: Machine learning models for satisfaction prediction

### Analysis Dimensions
- **Class Distribution**: Business, Economy, and Economy Plus passenger analysis
- **Demographics**: Gender and customer type (loyal vs. disloyal) patterns
- **Travel Patterns**: Business vs. Personal travel satisfaction comparison
- **Age Demographics**: Age-based satisfaction distribution
- **Service Ratings**: Detailed ratings for 9 different service categories (scale 1-5)

## 🤖 Machine Learning Components

### Models & Analysis
This project leverages machine learning for passenger satisfaction prediction:

#### Classification Models
- **Support Vector Machine (SVM)**: Primary classification algorithm for satisfaction prediction
- **Model Training**: Implemented in Jupyter notebooks with comprehensive data preprocessing
- **Features Used**: Multiple passenger attributes including demographics, travel class, service ratings
- **Binary Classification**: Predicts satisfied vs. dissatisfied passengers

#### Data Science Pipeline
1. **Data Collection**: Invistico Airline dataset with passenger feedback
2. **Preprocessing**: 
   - Label encoding for categorical variables
   - Data cleaning and normalization
   - Train-test split for model validation
3. **Model Training**: SVM classifier with optimized hyperparameters
4. **Evaluation**: Accuracy metrics and validation testing
5. **Deployment**: Serialized model (.sav file) for production use

#### ML Concepts Applied
- **Supervised Learning**: Classification based on labeled training data
- **Feature Engineering**: Transformation of categorical data to numerical format
- **Cross-validation**: Train-test split methodology
- **Model Persistence**: Pickle serialization for deployment
- **Data Aggregation**: Statistical grouping and analysis
- **Pattern Recognition**: Identifying satisfaction trends across dimensions

## 🏗️ Architecture

### Project Structure

```
air-passenger-sat/
├── src/
│   ├── app.py                 # Dash application initialization
│   ├── index.py               # Main entry point with routing
│   ├── config/
│   │   ├── __init__.py
│   │   └── constants.py       # Centralized configuration constants
│   ├── utils/
│   │   ├── __init__.py
│   │   └── data_utils.py      # Data loading and preprocessing utilities
│   ├── pages/
│   │   ├── __init__.py
│   │   ├── classification.py  # Categorical analysis page
│   │   └── pie_chart.py       # Ratings visualization page
│   ├── models/
│   │   ├── Classification_Model_new_SVM_Complted.ipynb  # ML model development
│   │   ├── Classification_Model_new.ipynb               # Initial model experiments
│   │   ├── Invistico_Airline_initial.sav                # Serialized dataset
│   │   └── Invistico_Airline.csv                        # Raw data
│   └── assets/
│       ├── association.css    # Custom styles
│       └── icon.png           # Application logo
├── env/                       # Virtual environment (Python 3.8)
├── requirements.txt           # Python dependencies
├── Procfile                   # Heroku deployment configuration
├── runtime.txt                # Python version specification
└── README.md                  # Project documentation
```

### Architecture Highlights
- **MVC Pattern**: Separation of data, presentation, and application logic
- **Modular Design**: Pages and utilities are independently maintainable
- **Configuration Management**: Centralized constants for easy customization
- **Single Page Application**: Client-side routing with URL path management

## 🚀 Getting Started

### Prerequisites

- **Python**: 3.8 or higher
- **pip**: Package manager
- **Virtual Environment**: Recommended for dependency isolation

### Installation

1. **Clone the repository**:
```bash
git clone <repository-url>
cd air-passenger-sat
```

2. **Activate the virtual environment**:
```bash
source env/bin/activate  # Linux/Mac
# or
env\Scripts\activate     # Windows
```

3. **Install dependencies**:
```bash
pip install -r requirements.txt
```

### Running the Application

#### Local Development

```bash
python src/index.py
```

The application will be available at `http://127.0.0.2:8050`

#### Production Deployment

The application is configured for deployment on platforms like Heroku:

```bash
gunicorn src.index:server
```

## 💻 Technologies Used

### Core Framework & Web Technologies
- **Dash (3.2.0)**: Python framework for building analytical web applications
- **Flask (3.0.3)**: Underlying WSGI web application framework
- **Dash Bootstrap Components (1.6.0)**: Bootstrap 5 components for Dash
- **Plotly (6.3.1)**: Interactive graphing library for Python
- **Dash Cytoscape (1.0.2)**: Network visualization components

### Data Science & Machine Learning
- **pandas (1.5.3)**: Data manipulation and analysis
- **NumPy (1.24.4)**: Numerical computing library
- **scikit-learn (1.3.2)**: Machine learning algorithms and tools
  - SVM (Support Vector Machine) for classification
  - Model selection and preprocessing utilities
  - Train-test split functionality
- **SciPy (1.10.1)**: Scientific computing library
- **statsmodels (0.14.1)**: Statistical modeling and testing

### Data Visualization
- **Matplotlib (3.7.5)**: Publication quality figures
- **Plotly Express (0.4.1)**: High-level Plotly interface
- **mlxtend (0.23.4)**: Machine learning extensions and utilities

### Production & Deployment
- **Gunicorn (23.0.0)**: Python WSGI HTTP Server for UNIX
- **Flask-Compress (1.15)**: Compress Flask responses
- **Werkzeug (3.0.6)**: WSGI utility library

### Additional Libraries
- **joblib (1.4.2)**: Model serialization and parallel computing
- **python-dateutil (2.9.0)**: Date parsing and manipulation
- **pytz (2025.2)**: Timezone definitions
- **requests (2.32.4)**: HTTP library for Python

### UI/UX Technologies
- **Bootstrap 5**: Responsive design framework (via Dash Bootstrap Components)
- **Bootswatch LUX Theme**: Professional Bootstrap theme
- **Custom CSS**: Additional styling for enhanced user experience
- **Responsive Design**: Mobile-first approach with viewport optimization

## 📊 Features

### 1. Categorical Visualization Page (`/classification`)

Interactive analytics dashboard focusing on categorical passenger attributes:

#### Age Distribution Analysis
- **Dynamic Histograms**: Age-based satisfaction visualization filtered by class
- **Class Selector**: Dropdown to filter by Business, Economy, or Economy Plus
- **Color-coded Visualization**: Age groups represented with distinct colors
- **Interactive Tooltips**: Hover details for precise data points

#### Satisfaction by Travel Class
- **Comparative Bar Charts**: Side-by-side comparison of satisfied vs. dissatisfied passengers
- **Faceted Views**: Separate panels for each travel class
- **Passenger Count Metrics**: Absolute numbers for data-driven insights

#### Customer Type Analysis
- **Loyalty Segmentation**: Loyal vs. Disloyal customer satisfaction patterns
- **Grouped Bar Charts**: Multiple dimensions in single visualization
- **Class-wise Breakdown**: Each travel class analyzed separately

#### Gender-based Analysis
- **Gender Distribution**: Male vs. Female satisfaction comparison
- **Multi-faceted Views**: Gender patterns across all travel classes
- **Grouped Visualizations**: Color-coded satisfaction levels

#### Travel Purpose Analysis
- **Business vs. Personal Travel**: Satisfaction patterns by travel type
- **Cross-class Comparison**: How travel purpose affects satisfaction in each class
- **Statistical Insights**: Count-based metrics for decision making

### 2. Ratings Visualization Page (`/pie_chart`)

Comprehensive service quality dashboard with nine rating categories:

#### Service Categories (1-5 Scale)
1. **Seat Comfort**: Physical comfort and seat quality ratings
2. **Inflight WiFi Service**: Internet connectivity and speed satisfaction
3. **Inflight Entertainment**: Content quality and system usability
4. **Online Support**: Customer service accessibility and quality
5. **Ease of Online Booking**: Booking system user experience
6. **Online Boarding**: Digital boarding process efficiency
7. **Leg Room Service**: Space and comfort metrics
8. **Cleanliness**: Aircraft and facility hygiene standards
9. **Food and Drink**: In-flight catering quality

#### Visualization Features
- **Interactive Pie Charts**: Proportional representation of rating distributions
- **3x3 Grid Layout**: Organized, scannable interface
- **Percentage Displays**: Exact proportions for each rating level
- **Hover Interactions**: Detailed breakdown on mouse hover
- **Dark Theme**: Professional plotly_dark theme for reduced eye strain

### Common Features Across Pages
- **Real-time Interactivity**: Instant updates based on user selections
- **Responsive Layout**: Adapts to different screen sizes (mobile, tablet, desktop)
- **Professional Navigation**: Consistent navbar with dropdown menu
- **Custom Branding**: Air U.S. logo and branded color scheme
- **Smooth Transitions**: Animated chart updates
- **Data Caching**: Optimized performance with pre-loaded data

## 🔧 Technical Details

### Application Architecture

#### Frontend Layer
- **Dash Framework**: Reactive Python framework for building web applications
- **Component-based Design**: Reusable UI components via Dash Bootstrap
- **Client-side Callbacks**: Real-time interactivity without page reloads
- **URL Routing**: Multi-page application with clean URL paths

#### Data Layer
- **Pickle Serialization**: Efficient data storage and loading
- **pandas DataFrames**: In-memory data manipulation
- **Pre-aggregated Data**: Computed statistics for faster rendering
- **Type-safe Operations**: Robust data transformation pipeline

#### Visualization Layer
- **Plotly.js**: WebGL-accelerated graphics rendering
- **Plotly Express**: High-level plotting API
- **Responsive Charts**: Automatic scaling and layout adjustment
- **Theme Consistency**: Unified dark theme across all visualizations

### Key Components

#### Data Processing (`src/utils/data_utils.py`)
```python
# Core Functionalities:
- load_airline_data(): Pickle file loading with error handling
- preprocess_airline_data(): Label encoding and data transformation
- get_processed_airline_data(): Combined loading and preprocessing
- aggregate_satisfaction_by_*(): Pre-computed aggregations for visualizations
- aggregate_ratings_by_category(): Service rating distributions
```

**Data Transformations**:
- Class codes (1,2,3) → Descriptive labels (business, eco, eco_plus)
- Satisfaction codes (0,1) → Labels (dissatisfied, satisfied)
- Gender codes (1,2) → Labels (male, female)
- Customer type codes (0,1) → Labels (loyal, disloyal)
- Travel type codes (1,2) → Labels (business travel, personal travel)

#### Configuration Management (`src/config/constants.py`)
```python
# Centralized Configuration:
- DATA_FILE_PATH: Dataset location
- CLASS_MAPPINGS: Numeric to text conversions
- SATISFACTION_MAPPINGS: Binary satisfaction labels
- PLOTLY_THEME: Visual theme selection
- RATING_COLUMNS: Service category definitions
- CHART_TITLES: Display text for visualizations
- NAVBAR_CONFIG: Branding and navigation settings
```

**Benefits**:
- Single source of truth for configuration
- Easy modification without code changes
- Consistent mappings across application
- Simplified testing and maintenance

#### Page Modules (`src/pages/`)

**Classification Page Features**:
- Module-level data loading (load once, use multiple times)
- Five separate callback functions for different visualizations
- Dynamic filtering based on user selection
- Pre-aggregated data for optimal performance

**Ratings Page Features**:
- Nine synchronized pie chart updates
- Single callback for all charts (efficient rendering)
- Pre-computed rating distributions
- Consistent chart generation function

### Performance Optimizations

1. **Data Loading Strategy**
   - Data loaded once at module import
   - Preprocessing performed once upfront
   - No redundant file I/O operations
   - Reduced memory allocation

2. **Pre-aggregation**
   - Common grouping operations computed once
   - Reusable aggregated DataFrames
   - Faster callback execution
   - Reduced computational overhead

3. **Callback Optimization**
   - Minimal computation in callbacks
   - Pre-processed data structures
   - Efficient Plotly figure creation
   - Suppressed unnecessary validation

4. **Code Quality**
   - Type hints for better IDE support
   - Comprehensive docstrings
   - Named constants (no magic numbers)
   - DRY principle throughout
   - Clean, readable formatting

### Data Pipeline

```
Raw Data (CSV) 
    ↓
Pickle Serialization (.sav)
    ↓
Load into pandas DataFrame
    ↓
Label Encoding & Preprocessing
    ↓
Pre-aggregation for Visualizations
    ↓
Dash Callbacks (user interaction)
    ↓
Plotly Figure Generation
    ↓
Interactive Web Display
```

### Security & Best Practices

- **No exposed credentials**: Environment-based configuration
- **Input validation**: Dropdown constraints prevent invalid inputs
- **Error handling**: Try-catch blocks in data loading
- **WSGI compliance**: Production-ready server (Gunicorn)
- **Compression**: Flask-Compress for reduced bandwidth
- **Static assets**: Efficient serving via assets folder

## 🛠️ Configuration

### Modifying Constants

Edit `src/config/constants.py` to change:
- File paths
- Data mappings
- Chart themes and colors
- Navbar configuration
- Default values

### Adding New Features

1. **New Page**: Create a new module in `src/pages/`
2. **New Visualization**: Add to existing page modules
3. **New Data Processing**: Add functions to `src/utils/data_utils.py`
4. **New Route**: Add routing logic in `src/index.py`

## 📦 Dependencies

### Production Dependencies

#### Web Framework Stack
```
dash==3.2.0                          # Core framework
dash-bootstrap-components==1.6.0     # UI components
dash-core-components==2.0.0          # Essential Dash components
dash-html-components==2.0.0          # HTML components
dash-table==5.0.0                    # Table components
dash-cytoscape==1.0.2                # Network graphs
Flask==3.0.3                         # Underlying web framework
Flask-Compress==1.15                 # Response compression
Werkzeug==3.0.6                      # WSGI utilities
```

#### Data Science & ML
```
pandas==1.5.3                        # Data manipulation
numpy==1.24.4                        # Numerical operations
scikit-learn==1.3.2                  # ML algorithms (SVM)
scipy==1.10.1                        # Scientific computing
statsmodels==0.14.1                  # Statistical models
mlxtend==0.23.4                      # ML extensions
joblib==1.4.2                        # Model persistence
```

#### Visualization
```
plotly==6.3.1                        # Interactive plots
plotly-express==0.4.1                # High-level plotting
matplotlib==3.7.5                    # Static visualizations
contourpy==1.1.1                     # Contour calculations
```

#### Utilities & Support
```
gunicorn==23.0.0                     # Production server
python-dateutil==2.9.0.post0         # Date parsing
pytz==2025.2                         # Timezone support
requests==2.32.4                     # HTTP library
click==8.1.8                         # CLI framework
```

### Development Environment
- **Python**: 3.8.3 (specified in runtime.txt)
- **Virtual Environment**: env/ directory for isolation
- **Package Manager**: pip 
- **Total Dependencies**: 50+ packages with transitive dependencies

See `requirements.txt` for the complete dependency list with exact versions.

## 🚢 Deployment

### Heroku Deployment

The application is production-ready and configured for Heroku:

#### Configuration Files
1. **Procfile**: Defines the web process command
   ```
   web: gunicorn src.index:server
   ```

2. **runtime.txt**: Specifies Python version
   ```
   python-3.8.3
   ```

3. **requirements.txt**: Lists all dependencies with versions

#### Deployment Steps
```bash
# Login to Heroku
heroku login

# Create new Heroku app
heroku create your-app-name

# Deploy to Heroku
git push heroku main

# Open deployed application
heroku open
```

#### Environment Configuration
- **WSGI Server**: Gunicorn for production-grade request handling
- **Worker Processes**: Configured based on dyno type
- **Port Binding**: Automatic via Heroku's PORT environment variable
- **Static Assets**: Served efficiently via Flask

### Alternative Deployment Options

#### Docker Deployment
```dockerfile
# Example Dockerfile structure
FROM python:3.8-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["gunicorn", "src.index:server", "--bind", "0.0.0.0:8050"]
```

#### AWS/GCP/Azure
- Deploy using container services (ECS, Cloud Run, App Service)
- Configure load balancing for scalability
- Set up environment variables for configuration
- Enable HTTPS/SSL certificates

### Best Practices

✅ **Before Deployment**:
- Test application locally with `gunicorn src.index:server`
- Verify all dependencies in requirements.txt
- Check for hardcoded paths or credentials
- Test on target Python version (3.8.3)
- Validate responsive design on multiple devices

✅ **Post Deployment**:
- Monitor application logs: `heroku logs --tail`
- Set up error tracking (e.g., Sentry)
- Configure auto-scaling if needed
- Set up CI/CD pipeline for automated deployments
- Regular dependency updates for security patches

## 🛠️ Configuration & Customization

### Modifying Application Settings

#### Update Constants (`src/config/constants.py`)
```python
# File paths
DATA_FILE_PATH = "path/to/your/data.sav"

# Visual theme
PLOTLY_THEME = 'plotly_dark'  # or 'plotly', 'seaborn', etc.

# Navbar branding
NAVBAR_CONFIG = {
    'color': '#17252A',
    'brand': 'Your Brand',
    'logo_height': '80px',
    'logo_path': '/assets/your-logo.png'
}

# App configuration
APP_CONFIG = {
    'host': '127.0.0.1',
    'debug': False  # Set to False in production
}
```

### Adding New Features

#### 1. Create New Page
```python
# Create src/pages/new_page.py
import dash_html_components as html
from src.app import app

layout = html.Div([
    # Your layout here
])

# Add callbacks
@app.callback(...)
def update_chart(...):
    # Your logic here
    pass
```

#### 2. Add Route
```python
# Update src/index.py
from src.pages import new_page

@app.callback(...)
def display_page(pathname):
    if pathname == '/new-page':
        return new_page.layout
    # ... existing routes
```

#### 3. Add Navigation Link
```python
# Update dropdown in src/index.py
dropdown = dbc.DropdownMenu(
    children=[
        dbc.DropdownMenuItem("Categorical Visualization", href="/classification"),
        dbc.DropdownMenuItem("Ratings", href="/pie_chart"),
        dbc.DropdownMenuItem("New Page", href="/new-page"),  # Add this
    ],
    # ... rest of config
)
```

### Customizing Visualizations

#### Change Chart Colors
```python
# In page modules
fig = px.bar(data, color_discrete_sequence=['#FF6B6B', '#4ECDC4', '#45B7D1'])
```

#### Modify Chart Layout
```python
fig.update_layout(
    title="Custom Title",
    xaxis_title="Custom X Label",
    yaxis_title="Custom Y Label",
    font=dict(size=14, family="Arial")
)
```

### Data Source Updates

To use different data:
1. Replace `src/models/Invistico_Airline_initial.sav` with your pickle file
2. Update column mappings in `src/config/constants.py`
3. Adjust aggregation functions in `src/utils/data_utils.py` if needed

## 📚 Project Structure Details

### Directory Breakdown

```
src/
├── app.py              # Dash app initialization, server configuration
├── index.py            # Routing, navigation, main entry point
├── config/             # Configuration management
│   └── constants.py    # All configurable values
├── utils/              # Utility functions
│   └── data_utils.py   # Data loading and processing
├── pages/              # Page components
│   ├── classification.py  # Multi-dimensional analysis
│   └── pie_chart.py       # Service ratings
├── models/             # ML models and data
│   ├── *.ipynb         # Jupyter notebooks for ML
│   ├── *.sav           # Serialized data/models
│   └── *.csv           # Raw datasets
└── assets/             # Static files (CSS, images)
```

### File Responsibilities

- **app.py**: Application initialization only
- **index.py**: Routing and navigation logic
- **constants.py**: All configurable values
- **data_utils.py**: All data operations
- **classification.py**: Categorical visualizations
- **pie_chart.py**: Rating distributions
- **assets/**: Styling and branding

## 🧪 Development Workflow

### Local Development

1. **Activate virtual environment**:
   ```bash
   source env/bin/activate
   ```

2. **Run in debug mode**:
   ```bash
   python src/index.py
   ```
   - Hot reloading enabled
   - Detailed error messages
   - Access at http://127.0.0.2:8050

3. **Test with production server**:
   ```bash
   gunicorn src.index:server --bind 127.0.0.1:8050
   ```

### Adding Dependencies

```bash
# Install new package
pip install package-name

# Update requirements.txt
pip freeze > requirements.txt

# Or manually add to requirements.txt with version pinning
echo "package-name==x.y.z" >> requirements.txt
```

### Code Style Guidelines

- **Docstrings**: All functions should have clear docstrings
- **Type Hints**: Use where applicable for better code clarity
- **Constants**: Define in `constants.py`, never hardcode
- **Naming**: 
  - Functions: `snake_case`
  - Classes: `PascalCase`
  - Constants: `UPPER_SNAKE_CASE`
- **Imports**: Group by standard library, third-party, local

## � Data Science Insights

### Dataset Characteristics

- **Source**: Invistico Airline passenger satisfaction survey
- **Format**: Serialized pickle file (.sav)
- **Features**: 
  - Demographic: Age, Gender
  - Customer: Customer Type (Loyal/Disloyal)
  - Travel: Class, Type of Travel
  - Ratings: 9 service categories (1-5 scale)
  - Target: Satisfaction (Binary: Satisfied/Dissatisfied)

### Machine Learning Workflow

```
1. Data Collection
   ↓
2. Exploratory Data Analysis (EDA)
   - Distribution analysis
   - Correlation studies
   - Feature importance
   ↓
3. Data Preprocessing
   - Label encoding
   - Normalization
   - Train-test split
   ↓
4. Model Training (SVM)
   - Hyperparameter tuning
   - Cross-validation
   - Performance evaluation
   ↓
5. Model Serialization
   - Save as .sav file
   - Deploy in production
   ↓
6. Visualization & Insights
   - Interactive dashboard
   - Real-time analytics
```

### Key Statistical Methods

- **Aggregation**: GroupBy operations for categorical analysis
- **Distribution Analysis**: Histograms and frequency distributions
- **Comparative Analysis**: Side-by-side group comparisons
- **Proportional Analysis**: Pie charts for rating distributions
- **Multi-dimensional Analysis**: Faceted visualizations

### Business Intelligence Insights

The dashboard enables stakeholders to:
- Identify service improvement areas based on low ratings
- Understand satisfaction patterns across customer segments
- Compare satisfaction between business and leisure travelers
- Analyze loyalty patterns and their impact on satisfaction
- Make data-driven decisions for service optimization


### Acknowledgments

- **Bootstrap Theme**: [Bootswatch LUX](https://bootswatch.com/lux/) - Modern, professional design
- **Dash Bootstrap Components**: [Documentation](https://dash-bootstrap-components.opensource.faculty.ai/)
- **Plotly**: [Documentation](https://plotly.com/python/)
- **scikit-learn**: [Documentation](https://scikit-learn.org/)
- **Invistico Airline Dataset**: Source of passenger satisfaction data

## 🔮 Future Enhancements

Potential features for future development:

- [ ] **Predictive Features**: Real-time satisfaction prediction interface
- [ ] **Advanced Analytics**: Time-series analysis if temporal data available
- [ ] **Comparison Tools**: Compare multiple airlines or time periods
- [ ] **Export Functionality**: Download charts as images or PDFs
- [ ] **Admin Dashboard**: Data upload and management interface
- [ ] **API Integration**: RESTful API for external data access
- [ ] **Enhanced ML Models**: Try Random Forest, XGBoost, Neural Networks
- [ ] **User Authentication**: Secure login for personalized views
- [ ] **Real-time Updates**: Live data streaming and updates
- [ ] **Mobile App**: Native mobile application version
- [ ] **A/B Testing**: Compare different UI/UX variations
- [ ] **Natural Language Processing**: Analyze text feedback if available

---

**Built with ❤️ using Python, Dash, and Machine Learning**

*Last Updated: October 2025*
