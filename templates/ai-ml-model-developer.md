---
title: "AI/ML Model Developer"
description: "Design, train, and deploy machine learning models with proper evaluation and monitoring"
category: "template-prompt"
tags: ["machine-learning", "ai", "data-science", "tensorflow", "pytorch", "model-deployment"]
tech_stack: ["python", "tensorflow", "pytorch", "scikit-learn", "mlflow"]
---

# AI/ML Model Developer

As a machine learning engineer, your role focuses on developing, training, and deploying machine learning models to be used in real-world applications.

## ML Project Requirements
- **Problem Type**: [INSERT TYPE - classification, regression, clustering, NLP, computer vision]
- **Data Source**: [INSERT SOURCE - CSV, database, API, real-time stream]
- **Model Framework**: [INSERT FRAMEWORK - TensorFlow, PyTorch, scikit-learn, XGBoost]
- **Performance Requirements**: [INSERT METRICS - accuracy, latency, throughput]
- **Deployment Target**: [INSERT TARGET - cloud, edge, mobile, API]
- **Scale**: [INSERT SCALE - batch processing, real-time inference, high-volume]

## Project Specifications
[INSERT DETAILED ML PROBLEM DESCRIPTION AND REQUIREMENTS]

## Output Format

### Data Pipeline and Preprocessing

```python
# data_pipeline.py
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler, LabelEncoder, OneHotEncoder
from sklearn.impute import SimpleImputer
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
import joblib
import logging

logger = logging.getLogger(__name__)

class DataPreprocessor:
    def __init__(self, config: dict):
        self.config = config
        self.preprocessor = None
        self.label_encoder = None
        self.feature_columns = None
        self.target_column = config.get('target_column', 'target')
        
    def load_data(self, file_path: str) -> pd.DataFrame:
        """Load data from various sources"""
        try:
            if file_path.endswith('.csv'):
                df = pd.read_csv(file_path)
            elif file_path.endswith('.parquet'):
                df = pd.read_parquet(file_path)
            elif file_path.endswith('.json'):
                df = pd.read_json(file_path)
            else:
                raise ValueError(f"Unsupported file format: {file_path}")
            
            logger.info(f"Loaded data: {df.shape}")
            return df
        except Exception as e:
            logger.error(f"Error loading data: {e}")
            raise
    
    def explore_data(self, df: pd.DataFrame) -> dict:
        """Generate data exploration insights"""
        exploration = {
            'shape': df.shape,
            'columns': df.columns.tolist(),
            'dtypes': df.dtypes.to_dict(),
            'missing_values': df.isnull().sum().to_dict(),
            'duplicate_rows': df.duplicated().sum(),
            'numeric_summary': df.describe().to_dict(),
            'categorical_info': {}
        }
        
        # Categorical column analysis
        categorical_cols = df.select_dtypes(include=['object']).columns
        for col in categorical_cols:
            exploration['categorical_info'][col] = {
                'unique_count': df[col].nunique(),
                'top_values': df[col].value_counts().head().to_dict()
            }
        
        return exploration
    
    def clean_data(self, df: pd.DataFrame) -> pd.DataFrame:
        """Clean and prepare data"""
        # Remove duplicates
        df = df.drop_duplicates()
        
        # Handle outliers for numeric columns
        numeric_columns = df.select_dtypes(include=[np.number]).columns
        for col in numeric_columns:
            if col != self.target_column:
                Q1 = df[col].quantile(0.25)
                Q3 = df[col].quantile(0.75)
                IQR = Q3 - Q1
                lower_bound = Q1 - 1.5 * IQR
                upper_bound = Q3 + 1.5 * IQR
                
                # Cap outliers instead of removing
                df[col] = df[col].clip(lower=lower_bound, upper=upper_bound)
        
        # Remove rows with missing target values
        df = df.dropna(subset=[self.target_column])
        
        logger.info(f"Data after cleaning: {df.shape}")
        return df
    
    def create_preprocessor(self, df: pd.DataFrame):
        """Create sklearn preprocessing pipeline"""
        # Identify column types
        numeric_features = df.select_dtypes(include=[np.number]).columns.tolist()
        categorical_features = df.select_dtypes(include=['object']).columns.tolist()
        
        # Remove target column from features
        if self.target_column in numeric_features:
            numeric_features.remove(self.target_column)
        if self.target_column in categorical_features:
            categorical_features.remove(self.target_column)
        
        self.feature_columns = numeric_features + categorical_features
        
        # Create preprocessing pipelines
        numeric_transformer = Pipeline(steps=[
            ('imputer', SimpleImputer(strategy='median')),
            ('scaler', StandardScaler())
        ])
        
        categorical_transformer = Pipeline(steps=[
            ('imputer', SimpleImputer(strategy='constant', fill_value='missing')),
            ('onehot', OneHotEncoder(handle_unknown='ignore', sparse_output=False))
        ])
        
        # Combine preprocessing steps
        self.preprocessor = ColumnTransformer(
            transformers=[
                ('num', numeric_transformer, numeric_features),
                ('cat', categorical_transformer, categorical_features)
            ]
        )
        
        # Handle target encoding for classification
        if self.config.get('problem_type') == 'classification':
            self.label_encoder = LabelEncoder()
    
    def fit_transform(self, df: pd.DataFrame):
        """Fit preprocessor and transform data"""
        # Prepare features and target
        X = df[self.feature_columns]
        y = df[self.target_column]
        
        # Transform features
        X_transformed = self.preprocessor.fit_transform(X)
        
        # Transform target for classification
        if self.label_encoder:
            y_transformed = self.label_encoder.fit_transform(y)
        else:
            y_transformed = y.values
        
        return X_transformed, y_transformed
    
    def transform(self, df: pd.DataFrame):
        """Transform new data using fitted preprocessor"""
        X = df[self.feature_columns]
        X_transformed = self.preprocessor.transform(X)
        
        if self.target_column in df.columns:
            y = df[self.target_column]
            if self.label_encoder:
                y_transformed = self.label_encoder.transform(y)
            else:
                y_transformed = y.values
            return X_transformed, y_transformed
        
        return X_transformed
    
    def save_preprocessor(self, path: str):
        """Save preprocessor and encoders"""
        preprocessor_data = {
            'preprocessor': self.preprocessor,
            'label_encoder': self.label_encoder,
            'feature_columns': self.feature_columns,
            'config': self.config
        }
        joblib.dump(preprocessor_data, path)
        logger.info(f"Preprocessor saved to {path}")
    
    def load_preprocessor(self, path: str):
        """Load preprocessor and encoders"""
        preprocessor_data = joblib.load(path)
        self.preprocessor = preprocessor_data['preprocessor']
        self.label_encoder = preprocessor_data['label_encoder']
        self.feature_columns = preprocessor_data['feature_columns']
        self.config = preprocessor_data['config']
        logger.info(f"Preprocessor loaded from {path}")

def prepare_data(config: dict):
    """Main data preparation function"""
    preprocessor = DataPreprocessor(config)
    
    # Load and explore data
    df = preprocessor.load_data(config['data_path'])
    exploration = preprocessor.explore_data(df)
    logger.info(f"Data exploration: {exploration}")
    
    # Clean data
    df_clean = preprocessor.clean_data(df)
    
    # Create and fit preprocessor
    preprocessor.create_preprocessor(df_clean)
    X, y = preprocessor.fit_transform(df_clean)
    
    # Split data
    X_train, X_test, y_train, y_test = train_test_split(
        X, y, 
        test_size=config.get('test_size', 0.2),
        random_state=config.get('random_state', 42),
        stratify=y if config.get('problem_type') == 'classification' else None
    )
    
    # Save preprocessor
    preprocessor.save_preprocessor(config.get('preprocessor_path', 'preprocessor.joblib'))
    
    return {
        'X_train': X_train, 'X_test': X_test,
        'y_train': y_train, 'y_test': y_test,
        'preprocessor': preprocessor,
        'exploration': exploration
    }
```

### Model Development and Training

```python
# model_trainer.py
import tensorflow as tf
import torch
import torch.nn as nn
from sklearn.ensemble import RandomForestClassifier, RandomForestRegressor
from sklearn.linear_model import LogisticRegression, LinearRegression
from sklearn.svm import SVC, SVR
from sklearn.metrics import classification_report, mean_squared_error, r2_score
import mlflow
import mlflow.tensorflow
import mlflow.pytorch
import mlflow.sklearn
from typing import Any, Dict, Tuple
import numpy as np

class ModelTrainer:
    def __init__(self, config: dict):
        self.config = config
        self.model = None
        self.history = None
        
        # Initialize MLflow
        mlflow.set_experiment(config.get('experiment_name', 'ml_experiment'))
    
    def create_tensorflow_model(self, input_shape: int, num_classes: int = None) -> tf.keras.Model:
        """Create TensorFlow/Keras model"""
        model = tf.keras.Sequential([
            tf.keras.layers.Dense(128, activation='relu', input_shape=(input_shape,)),
            tf.keras.layers.Dropout(0.3),
            tf.keras.layers.Dense(64, activation='relu'),
            tf.keras.layers.Dropout(0.3),
            tf.keras.layers.Dense(32, activation='relu'),
        ])
        
        if self.config['problem_type'] == 'classification':
            if num_classes > 2:
                model.add(tf.keras.layers.Dense(num_classes, activation='softmax'))
                model.compile(
                    optimizer='adam',
                    loss='sparse_categorical_crossentropy',
                    metrics=['accuracy']
                )
            else:
                model.add(tf.keras.layers.Dense(1, activation='sigmoid'))
                model.compile(
                    optimizer='adam',
                    loss='binary_crossentropy',
                    metrics=['accuracy']
                )
        else:  # regression
            model.add(tf.keras.layers.Dense(1))
            model.compile(
                optimizer='adam',
                loss='mse',
                metrics=['mae']
            )
        
        return model
    
    def create_pytorch_model(self, input_size: int, num_classes: int = None) -> nn.Module:
        """Create PyTorch model"""
        class NeuralNetwork(nn.Module):
            def __init__(self, input_size, num_classes=None):
                super().__init__()
                self.fc1 = nn.Linear(input_size, 128)
                self.fc2 = nn.Linear(128, 64)
                self.fc3 = nn.Linear(64, 32)
                
                if self.config['problem_type'] == 'classification':
                    self.output = nn.Linear(32, num_classes if num_classes > 2 else 1)
                else:
                    self.output = nn.Linear(32, 1)
                
                self.dropout = nn.Dropout(0.3)
                self.relu = nn.ReLU()
            
            def forward(self, x):
                x = self.relu(self.fc1(x))
                x = self.dropout(x)
                x = self.relu(self.fc2(x))
                x = self.dropout(x)
                x = self.relu(self.fc3(x))
                x = self.output(x)
                return x
        
        return NeuralNetwork(input_size, num_classes)
    
    def create_sklearn_model(self):
        """Create scikit-learn model"""
        if self.config['problem_type'] == 'classification':
            if self.config.get('model_type') == 'random_forest':
                return RandomForestClassifier(
                    n_estimators=100,
                    random_state=42,
                    n_jobs=-1
                )
            elif self.config.get('model_type') == 'logistic_regression':
                return LogisticRegression(random_state=42, max_iter=1000)
            elif self.config.get('model_type') == 'svm':
                return SVC(random_state=42)
        else:  # regression
            if self.config.get('model_type') == 'random_forest':
                return RandomForestRegressor(
                    n_estimators=100,
                    random_state=42,
                    n_jobs=-1
                )
            elif self.config.get('model_type') == 'linear_regression':
                return LinearRegression()
            elif self.config.get('model_type') == 'svm':
                return SVR()
    
    def train_model(self, X_train: np.ndarray, y_train: np.ndarray, 
                   X_val: np.ndarray = None, y_val: np.ndarray = None) -> Any:
        """Train the model based on framework"""
        
        with mlflow.start_run():
            # Log parameters
            mlflow.log_params(self.config)
            
            framework = self.config.get('framework', 'sklearn')
            
            if framework == 'tensorflow':
                self.model = self.create_tensorflow_model(
                    X_train.shape[1], 
                    len(np.unique(y_train)) if self.config['problem_type'] == 'classification' else None
                )
                
                callbacks = [
                    tf.keras.callbacks.EarlyStopping(patience=10, restore_best_weights=True),
                    tf.keras.callbacks.ReduceLROnPlateau(patience=5, factor=0.5)
                ]
                
                validation_data = (X_val, y_val) if X_val is not None else None
                
                self.history = self.model.fit(
                    X_train, y_train,
                    epochs=self.config.get('epochs', 100),
                    batch_size=self.config.get('batch_size', 32),
                    validation_data=validation_data,
                    callbacks=callbacks,
                    verbose=1
                )
                
                # Log model
                mlflow.tensorflow.log_model(self.model, "model")
                
            elif framework == 'pytorch':
                # PyTorch training implementation
                self.model = self.create_pytorch_model(
                    X_train.shape[1],
                    len(np.unique(y_train)) if self.config['problem_type'] == 'classification' else None
                )
                
                # Training loop would go here
                self._train_pytorch_model(X_train, y_train, X_val, y_val)
                
                # Log model
                mlflow.pytorch.log_model(self.model, "model")
                
            else:  # sklearn
                self.model = self.create_sklearn_model()
                self.model.fit(X_train, y_train)
                
                # Log model
                mlflow.sklearn.log_model(self.model, "model")
            
            return self.model
    
    def _train_pytorch_model(self, X_train, y_train, X_val, y_val):
        """PyTorch specific training loop"""
        # Convert to tensors
        X_train_tensor = torch.FloatTensor(X_train)
        y_train_tensor = torch.LongTensor(y_train) if self.config['problem_type'] == 'classification' else torch.FloatTensor(y_train)
        
        # Define loss and optimizer
        if self.config['problem_type'] == 'classification':
            criterion = nn.CrossEntropyLoss() if len(np.unique(y_train)) > 2 else nn.BCEWithLogitsLoss()
        else:
            criterion = nn.MSELoss()
        
        optimizer = torch.optim.Adam(self.model.parameters(), lr=0.001)
        
        # Training loop
        epochs = self.config.get('epochs', 100)
        batch_size = self.config.get('batch_size', 32)
        
        for epoch in range(epochs):
            self.model.train()
            total_loss = 0
            
            # Mini-batch training
            for i in range(0, len(X_train_tensor), batch_size):
                batch_X = X_train_tensor[i:i+batch_size]
                batch_y = y_train_tensor[i:i+batch_size]
                
                optimizer.zero_grad()
                outputs = self.model(batch_X)
                loss = criterion(outputs.squeeze(), batch_y)
                loss.backward()
                optimizer.step()
                
                total_loss += loss.item()
            
            if epoch % 10 == 0:
                print(f'Epoch {epoch}, Loss: {total_loss/len(X_train_tensor):.4f}')
    
    def evaluate_model(self, X_test: np.ndarray, y_test: np.ndarray) -> Dict:
        """Evaluate model performance"""
        if self.config.get('framework') == 'tensorflow':
            predictions = self.model.predict(X_test)
            if self.config['problem_type'] == 'classification':
                y_pred = (predictions > 0.5).astype(int) if predictions.shape[1] == 1 else np.argmax(predictions, axis=1)
            else:
                y_pred = predictions.flatten()
        
        elif self.config.get('framework') == 'pytorch':
            self.model.eval()
            with torch.no_grad():
                X_test_tensor = torch.FloatTensor(X_test)
                predictions = self.model(X_test_tensor)
                if self.config['problem_type'] == 'classification':
                    y_pred = torch.argmax(predictions, dim=1).numpy()
                else:
                    y_pred = predictions.squeeze().numpy()
        
        else:  # sklearn
            y_pred = self.model.predict(X_test)
        
        # Calculate metrics
        if self.config['problem_type'] == 'classification':
            from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score
            
            metrics = {
                'accuracy': accuracy_score(y_test, y_pred),
                'precision': precision_score(y_test, y_pred, average='weighted'),
                'recall': recall_score(y_test, y_pred, average='weighted'),
                'f1_score': f1_score(y_test, y_pred, average='weighted')
            }
            
            # Log metrics
            mlflow.log_metrics(metrics)
            
            # Classification report
            report = classification_report(y_test, y_pred)
            print("Classification Report:")
            print(report)
            
        else:  # regression
            metrics = {
                'mse': mean_squared_error(y_test, y_pred),
                'rmse': np.sqrt(mean_squared_error(y_test, y_pred)),
                'r2_score': r2_score(y_test, y_pred)
            }
            
            # Log metrics
            mlflow.log_metrics(metrics)
            
            print(f"MSE: {metrics['mse']:.4f}")
            print(f"RMSE: {metrics['rmse']:.4f}")
            print(f"R² Score: {metrics['r2_score']:.4f}")
        
        return metrics
    
    def save_model(self, path: str):
        """Save trained model"""
        if self.config.get('framework') == 'tensorflow':
            self.model.save(path)
        elif self.config.get('framework') == 'pytorch':
            torch.save(self.model.state_dict(), path)
        else:  # sklearn
            import joblib
            joblib.dump(self.model, path)
        
        print(f"Model saved to {path}")
```

### Model Deployment and Serving

```python
# model_server.py