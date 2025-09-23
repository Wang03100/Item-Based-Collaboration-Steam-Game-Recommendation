# Steam Recommendation System

A scalable game recommendation engine built with item-based collaborative filtering, designed to handle large-scale Steam gaming data efficiently. Dataset from https://www.kaggle.com/datasets/antonkozyriev/game-recommendations-on-steam?select=recommendations.csv and SteamSpy API for metadata.

## Overview

This system processes millions of user-game interactions to generate personalized game recommendations. By leveraging sparse matrix operations and the SteamSpy API, it provides accurate recommendations while maintaining optimal memory usage.

## Why Item-Based Instead of User-Based

User-based is finding users with similar game preference and then suggesting game from that preference. The issue is game preferences change over time and there is around 1.58 million users. 1.58 M x 1.58 M ~= 200 GB of memory needed to calculate a similarity matrix.

Item-based is finding games thats similar to another game based on user interaction. This filtering was chosen as it ignores current trend and provides 20k x 20k ~= 132.7 MB of memory to calculate a similarity matrix.



## Disclaimer

Dataset range is limited to 2024 prior.

## Key Features

* **Large-scale data processing**: Handles 17.4M user-game interactions across 20,000+ games
* **Memory-efficient architecture**: Uses sparse matrices to reduce memory requirements from 200GB to ~133MB
* **API integration**: Automated SteamSpy API data collection with comprehensive error handling
* **Collaborative filtering**: Item-based KNN with cosine similarity for accurate recommendations
* **Rich metadata**: Returns game names, developers, and similarity scores for user-friendly results

## Technical Implementation

* **Data Pipeline**: Pandas-based ETL for cleaning and preprocessing interaction data
* **Matrix Operations**: scipy.sparse for memory-efficient collaborative filtering
* **Machine Learning**: scikit-learn KNN with cosine similarity metrics
* **API Integration**: Paginated SteamSpy API collection for complete metadata coverage

## Technology Stack

* **Python 3.8+**
* **pandas** - Data manipulation and analysis
* **numpy** - Numerical computing
* **scipy.sparse** - Sparse matrix operations
* **scikit-learn** - Machine learning algorithms
* **requests** - API integration
* **pickle** - Model serialization

## Dataset

* **Interactions**: 17.4 million user-game interaction records
* **Games**: 20,246 unique Steam games
* **Users**: 1,579,926 unique users
* **Metadata Coverage**: 91.8% complete game metadata from SteamSpy API
* **Matrix Sparsity**: ~99.6% sparse for memory efficiency

## Architecture

```
Input: game_id
├── Item-Based Collaborative Filtering (Primary)
│   ├── Sparse item-user matrix (20K × 1.5M)
│   ├── KNN with cosine similarity
│   └── Returns similar games based on user patterns
└── Content-Based Fallback (In Development)
    ├── SteamSpy genre lookup
    └── Popular games by genre
```

## Performance Metrics

* **Memory Usage**: ~133MB (sparse matrix storage)
* **Processing Time**: <2 seconds for recommendation generation
* **Accuracy**: Contextually relevant recommendations (e.g., Half-Life 2, Garry's Mod for Team Fortress 2)
* **Coverage**: 91.8% metadata completeness for rich user experience

## Current Status

**Phases 1-3 Complete:**
* Data collection and SteamSpy API integration
* Sparse matrix creation and optimization
* Item-based collaborative filtering implementation
* Metadata integration and rich recommendations

**In Development:**
* Content-based genre fallback system for unknown games
* FastAPI REST endpoint
* Comprehensive testing and validation

## Example Output

```python
# Input: Team Fortress 2 (game_id: 440)
# Output:
[
    {
        'app_id': 220,
        'name': 'Half-Life 2',
        'developer': 'Valve',
        'similarity_score': 0.847
    },
    {
        'app_id': 4000,
        'name': "Garry's Mod",
        'developer': 'Facepunch Studios',
        'similarity_score': 0.823
    }
    # ... 3 more recommendations
]
```

## Installation

```bash
# Clone repository
git clone https://github.com/Wang03100/Item-Based-Collaboration-Steam-Game-Recommendation.git
cd Item-Based-Collaboration-Steam-Game-Recommendation

# Create virtual environment
python -m venv .venv

# Activate virtual environment
# On Windows:
.venv\Scripts\activate
# On macOS/Linux:
source .venv/bin/activate

# Install dependencies
pip install pandas numpy scipy scikit-learn requests matplotlib

# Install kaggle dataset into data/ folder
https://www.kaggle.com/datasets/antonkozyriev/game-recommendations-on-steam?select=recommendations.csv
```

## File Structure

```
├── .venv/                         # Python virtual environment
├── data/
│   ├── recommendations.csv        # from https://www.kaggle.com/datasets/antonkozyriev/game-recommendations-on-steam?select=recommendations.csv
├── notebooks/
│                                  # Run ipynb in following order: data_cleaning, user_item_matrix, item_based_collab, fallback_genre_based
│   ├── data_cleaning.ipynb        # Data preprocessing and SteamSpy API integration
│   ├── user_item_matrix.ipynb     # Sparse matrix creation and optimization
│   └── item_based_collab.ipynb    # KNN collaborative filtering implementation
│   └── fallback_genre_based.ipynb # SteamSpy API content-based genre recommendation
└── README.md
```

## Contributing

This project demonstrates scalable recommendation systems, sparse matrix optimization, and large-scale data processing techniques. Contributions welcome for enhancing the content-based fallback system and API development.
