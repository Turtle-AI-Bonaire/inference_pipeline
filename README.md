# Tag-a-Turtle Project - Google Collab Turtle Recognition Pipeline
## Overview
The Tag-a-Turtle project aims to develop a machine learning pipeline that can identify individual sea turtles based on their facial features. This system will assist researchers in tracking turtles in a non-invasive manner, eliminating the need for physical tagging. The pipeline works by detecting turtle faces in images, converting them into embeddings, and then matching them to previously identified turtles.

This system is hosted and run on Google Colab and is designed to be scalable and modular, allowing easy updates and additions to the pipeline.

## Requirements
The system must meet the following technical and operational requirements:

### Environment: Google Colab (preferred by the stakeholders).

### Inputs

* **Gallery of turtle images**: Each image name contains the turtle's label.
* **Query folder**: Contains images that need to be matched with the gallery images.

### Outputs
A collage of images of matching turtles from the gallery, ranked by similarity.

### Modular Design
Easy to add models or processing steps to the pipeline.

### Scalability
Should accommodate growing datasets over time.

## Architecture
The system is structured to allow modularity, ensuring that each component can be updated or replaced easily.

### 1. Data Management
* **Image Dataset Folder**: Supports multiple folder structures, including flat structure or split by identity or year.
* **Query Folder**: Organized by individual turtle IDs, with each turtle's images stored in separate subdirectories.
* **Auto-generated Files**: Metadata annotations are automatically generated for the dataset and query folders, making it easy to load files regardless of their folder structure.
* **Embedding Storage**: Embeddings are stored in batches to speed up processing and avoid recomputing embeddings for the entire dataset each time.
### 2. Inference Pipeline
The inference pipeline processes a batch of images and applies necessary AI models to generate embeddings. Each function in this pipeline is focused on a single task for easy updates.

### 3. Models
* **Detection Model**: Identifies the region of interest (turtle's face) in images. Supported models include YOLOv8 or YOLO11.
* **Embedding Model**: Maps the detected face into a high-dimensional vector space, typically using a fine-tuned ResNet architecture. This model uses loss functions like Contrastive Loss, Proxy-Anchor Loss, or ArcFace Loss to improve the accuracy of the embeddings.
* **Embedding Aggregation**: If multiple images of the same turtle are available, their embeddings are averaged to create a more representative embedding, improving recognition accuracy.
### 4. Recognition and Visual Output
The recognition phase compares query embeddings with those in the database. The closest matches are ranked using a cosine similarity function. The system outputs a gallery of matching turtles, ranked by similarity, with visual results for easy interpretation.

## Features
* **Model Flexibility**: Easily swap out recognition models.
* **Data Loading Flexibility**: Change dataset formats with minimal effort due to decoupled dataset class.
* **Embedding Aggregation**: Optionally aggregate embeddings from multiple images for better recognition.
* **Top N Results**: Control how many matched images are returned for each turtle in the query.
## Setup and Usage
* Clone this repository to your Google Colab environment.
* Upload the image dataset and query images according to the specified folder and file paths, or modify them to your situation.
* Run the pipeline: Process images using the recognition and inference pipeline.
* Review the results: The system will output a collage of the most similar images from the gallery for each individual turtle in the query folder.