# End-to-End Content-Based Recommender System

A production-ready machine learning recommender system that leverages TF-IDF and content-based filtering to deliver personalized recommendations at scale.

## Overview

This project implements a complete end-to-end machine learning recommender system designed for production deployment. It combines data science best practices with modern microservices architecture to deliver scalable, personalized content recommendations.

**Key Capabilities:**
- Process and analyze user interaction data
- Extract meaningful content features using TF-IDF vectorization
- Generate personalized recommendations based on user profiles
- Serve predictions via RESTful API with sub-100ms latency
- Deploy containerized service to AWS ECS

## Key Features

✅ **Content-Based Filtering** - Sophisticated TF-IDF based recommendation engine  
✅ **Scalable Architecture** - Microservice design for easy scaling and maintenance  
✅ **Jupyter Notebooks** - Complete model development and feature engineering pipeline  
✅ **Dockerized Service** - Container-ready for cloud deployment  
✅ **REST API** - Simple HTTP endpoints for real-time predictions  
✅ **Pre-trained Models** - Serialized models for fast inference  
✅ **AWS Integration** - Ready for ECR and ECS deployment  


## Project Structure

```
├── notebook/
│   └── recommenderSystemNotebook.ipynb    # End-to-end model development
├── service/
│   ├── recommender_system_service.py      # Flask API service
│   ├── content_based_recommender.py       # Core recommendation logic
│   ├── Dockerfile                         # Container configuration
│   ├── content_based_recommender_model.p  # Trained model (pickle)
│   ├── tfidf_matrix.p                     # TF-IDF vectorizer
│   ├── user_profiles.p                    # User profile data
│   └── item_ids.p                         # Item ID mapping
├── archive/
│   ├── users_interactions.csv             # Historical interaction data
│   └── shared_articles.csv                # Article content features
├── docs/
│   └── ml-pipeline.png                    # Architecture diagram
├── README.md
└── requirements.txt
```

## Getting Started

### Installation

**1. Clone the Repository**
```bash
git clone https://github.com/AbdelkaderHamdi/end-to-end-ML-recommender-system.git
cd end-to-end-ML-recommender-system
```

**2. Set Up Virtual Environment (Windows)**
```bash
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
```

**3. Set Up Virtual Environment (macOS/Linux)**
```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

## Usage

### Local Testing

**1. Build Docker Image**
```bash
cd service
docker build -t content-base-recommender .
```

**2. Run Container**
```bash
docker run -d --publish 7777:5000 content-base-recommender
```

**3. Test the Service**
```bash
# Example API request (replace user_id with actual ID)
curl http://localhost:7777/recommend/-1479311724257856983
```

## API Documentation

### Recommendation Endpoint

**Request:**
```
GET /recommend/<user_id>
```

**Response:**
```json
{
  "user_id": "-1479311724257856983",
  "recommendations": [
    {"item_id": 1, "score": 0.95},
    {"item_id": 2, "score": 0.87}
  ]
}
```

## Machine Learning Pipeline

![ML Recommendation Pipeline](docs/ml-pipeline.png)

**Pipeline Steps:**
1. **Data Ingestion** - Load user interactions and article metadata
2. **Feature Engineering** - TF-IDF vectorization of content
3. **User Profiling** - Aggregate user interaction patterns
4. **Similarity Computation** - Calculate content similarity scores
5. **Recommendation Ranking** - Rank items by relevance
6. **API Serving** - Expose predictions via REST endpoint

## Deployment

### Deploy to AWS ECS

**1. Configure AWS Region**
```bash
aws configure set region eu-west-1
```

**2. Create ECR Repository**
```bash
aws ecr create-repository --region eu-west-1 --repository-name ecs-recommender-system/home
```

**3. Authenticate Docker with ECR**
```bash
aws ecr get-login-password --region eu-west-1 | docker login --username AWS --password-stdin 477557400504.dkr.ecr.eu-west-1.amazonaws.com
```

**4. Tag and Push Image**
```bash
docker tag content-base-recommender:latest 477557400504.dkr.ecr.eu-west-1.amazonaws.com/ecs-recommender-system/home:latest
docker push 477557400504.dkr.ecr.eu-west-1.amazonaws.com/ecs-recommender-system/home:latest
```

**5. Deploy to ECS** - Configure ECS task definition and service using the AWS Console or CLI.


## License

This project is available under the MIT License.

---

**Questions or contributions?** Feel free to open an issue or submit a pull request.