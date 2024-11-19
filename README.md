# cs_361_MicroA
Microservice A

Requesting Data
To request data from the microservice, follow these steps:

1. Start the Microservice
    Run the program:

    python app.py
    The service will start on http://127.0.0.1:5000.

2. Retrieve List of Games
    Send a GET request to /games:

    curl http://127.0.0.1:5000/games
    Example Response:

    [
        {"id": 1, "teams": "Team A vs Team B", "date": "2024-11-20", "status": "upcoming"},
        {"id": 2, "teams": "Team C vs Team D", "date": "2024-11-21", "status": "upcoming"}
    ]

3. Retrieve a Specific Prediction
    Send a GET request to /predictions/<game_id>:

    curl http://127.0.0.1:5000/predictions/1
    Example Response:

    {"user": "User1", "prediction": "Team A"}

Receiving Data

1. Create a Prediction
    Send a POST request with JSON data to /predictions:

    curl -X POST http://127.0.0.1:5000/predictions -H "Content-Type: application/json" -d '{
        "game_id": 3,
        "user": "User3",
        "prediction": "Team E"
             }'
    Example Response:

    {"message": "Prediction added successfully"}

2. Error Responses
    Requesting a prediction for a non-existent game:

        curl http://127.0.0.1:5000/predictions/999
    Response:

        {"error": "Prediction not found"}


3. Create a Prediction
    User -> Microservice: POST /predictions with JSON data
    Microservice -> Database: Add prediction to storage
    Database -> Microservice: Confirm addition
    Microservice -> User: Respond with success message

