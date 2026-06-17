# Image-Based Text Generation API with Vision-Language Model

This project provides a FastAPI-based REST API that generates text responses from images using a Vision-Language Model.

The application receives an image and a text question, processes both inputs with a pre-trained visual question answering model, and returns the predicted answer in JSON format.

## Project Objective

The main objective of this project is to demonstrate how to deploy a Vision-Language Model through an API.

The API allows users to:

* Send an image file to the API;
* Send a text question related to the image;
* Process image and text inputs together;
* Generate an answer using a pre-trained VQA model;
* Consume the API through a Python client;
* Run the project inside a Docker container.

## Technologies Used

* Python
* FastAPI
* Uvicorn
* Transformers
* PyTorch
* Pillow
* Requests
* Docker

## Project Structure

```text
.
├── main.py              # FastAPI application
├── modelo.py            # Vision-Language Model pipeline
├── cliente.py           # Python client to consume the API
├── Dockerfile           # Docker image configuration
├── LEIAME.txt           # Original execution instructions
├── imagem1.png          # Sample image
├── imagem2.png          # Sample image
└── imagem3.jpg          # Sample image
```

## How the Project Works

The project follows this workflow:

1. The API is started with FastAPI and Uvicorn;
2. The user sends a POST request to the `/api` endpoint;
3. The request must include:

   * A text question;
   * An image file;
4. The image is loaded and processed with Pillow;
5. The text and image are sent to the Vision-Language Model pipeline;
6. The model generates the most likely answer;
7. The API returns the result as a JSON response.

## Model

The project uses the following pre-trained model:

```text
dandelin/vilt-b32-finetuned-vqa
```

This model is designed for Visual Question Answering tasks, where the input consists of an image and a question, and the output is a text answer related to the image.

## API Endpoints

### GET `/`

Health check route used to verify whether the API is running.

#### Example Response

```json
{
  "DSA": "Projeto4"
}
```

### POST `/api`

Main endpoint used to send an image and a text question to the model.

#### Request Parameters

The endpoint expects a multipart form-data request with:

| Field   | Type   | Description               |
| ------- | ------ | ------------------------- |
| `text`  | string | Question about the image  |
| `image` | file   | Image file to be analyzed |

#### Example Questions

```text
Which color is the car in the image?
```

```text
Which color is the elephant in the image?
```

```text
What is the dog doing in the image?
```

#### Example Response

```json
{
  "Resposta": "eating"
}
```

## Running with Docker

From the project folder, build the Docker image:

```bash
docker build -t dsa-deploy:p4 .
```

Run the Docker container:

```bash
docker run -dit --name dsa-p4 -p 3000:3000 dsa-deploy:p4
```

Check the container logs to confirm that the API has started:

```bash
docker logs dsa-p4
```

The API will be available at:

```text
http://localhost:3000
```

## Running the Client

After starting the API container, run the client script:

```bash
python cliente.py
```

The client sends a text question and an image to the API and prints the JSON response returned by the model.

## Example Client Request

The client sends a request to:

```text
http://localhost:3000/api
```

Using a payload similar to:

```python
payload = {
    "text": (None, "What is the dog doing in the image?")
}
```

And an image file:

```python
file = [
    ("image", open("imagem3.jpg", "rb"))
]
```

## Notes

* The model is loaded from Hugging Face using the Transformers library.
* The first execution may take longer because the model needs to be downloaded.
* The API expects both a valid image and a text question.
* The project can be executed inside Docker for easier deployment and reproducibility.
* This project was developed for educational purposes and demonstrates how to deploy a Vision-Language Model as a REST API.

## Author

Project developed as a practical study on API deployment for image-based text generation using Vision-Language Models.
