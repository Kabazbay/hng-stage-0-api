# HNG Stage 0 - API Integration

This is a backend task for HNG API Integration. It is a single GET endpoint built using Node.js and Express that integrates with the external [Genderize API](https://genderize.io).

## Features
- **Classifies Names**: Accepts a `name` query parameter and fetches gender prediction from Genderize API.
- **Calculates Confidence**: Adds a computed `is_confident` boolean which is `true` if probability >= 0.7 AND sample size >= 100.
- **Date stamp**: Includes a dynamic ISO 8601 formatted UTC date upon request processing.
- **Robust Error Handling**: Properly handles missing logic, wrong data types, empty data API responses, and upstream failure (500) edge cases.
- **Cross-Origin Configuration**: Uses `cors` handling requests seamlessly.

## Tech Stack
- **Node.js**
- **Express**: Fast web framework for managing endpoints.
- **Axios**: Promised-based wrapper for simplified external API requests.
- **CORS**: Node.js plugin for setting up Access Allow headers.

## Getting Started Locally

### Prerequisites
Make sure you have [Node.js](https://nodejs.org/) installed on your machine.

### Installation

1. Copy/Clone this folder to your machine.
2. In the folder directory, install the required packages using:
   ```sh
   npm install
   ```

### Running the server

To power up the server, run:
```sh
node index.js
```

The server will be available at `http://localhost:3000`.

### Testing Output Format using `cURL` or Postman

#### Valid Request
```sh
curl http://localhost:3000/api/classify?name=john
```

**Response**:
```json
{
  "status": "success",
  "data": {
    "name": "john",
    "gender": "male",
    "probability": 0.99,
    "sample_size": 1234,
    "is_confident": true,
    "processed_at": "2026-04-01T12:00:00Z"
  }
}
```

#### Missing Parameter
```sh
curl http://localhost:3000/api/classify
```

**Response**:
```json
{
  "status": "error",
  "message": "Missing or empty name parameter"
}
```

#### No Prediction Given
```sh
curl http://localhost:3000/api/classify?name=xzytwqpd
```

**Response**:
```json
{
  "status": "error",
  "message": "No prediction available for the provided name"
}
```
