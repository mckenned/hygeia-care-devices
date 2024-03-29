# Medical Devices Backend

This repo contains the code for running the microservice for medical devices in the context of the hygena app.

## Running from a docker container

A docker image can be built from the exisitng docker file. Running the resulting image will run the medical devices on the port defined in the Dockerfile. 

This can be achieved in Visual Studio Code, or by running the following commands from the directory of the project:

```bash
docker build --pull --rm -f "Dockerfile" -t medicaldevices:latest "."

docker run -p <replace with MD_APP_PORT value>:<replace with MD_APP_PORT value> medicaldevices:latest

```

## Running Locally

The app can be started by running the following command and will run on port 3000 my default:

```bash
npm start
```
This will attempt a connection to a local database. To reach the mongodb database, define the environment variable

```bash
DB_URL="mongodb+srv://medDevService:lHFPV6sI94nny2cD@medicaldevicescluster.h2blqct.mongodb.net/?retryWrites=true&w=majority"
```

Optionally, the port to run the app on can be defined with the following environment variable:

```bash
MD_APP_PORT=3001
```

## Usage

The app supports two resources, "analysis" and "measurements". See below for examples of the supported requests:

```bash
# get all analysis
curl --location 'http://localhost:3001/api/v1/analysis'
# get specific analysis by id
curl --location 'http://localhost:5000/api/v1/analysis/<id>'
# filtered get analysis
curl --location 'http://localhost:3000/api/v1/analysis?userId=xxx'
# delete analysis
curl --location --request DELETE 'http://localhost:3000/api/v1/analysis/659966eea30e7700627e5e1a'
# post analysis
curl --location 'http://localhost:3000/api/v1/analysis' \
--header 'Content-Type: application/json' \
--data '{ "measurement": "659a89130ea326c42db23007", "value":"newVal2"}'

# get all measurement
curl --location 'http://localhost:3000/api/v1/measurement'
# post measurement
curl --location 'http://localhost:3000/api/v1/measurement' \
--header 'Content-Type: application/json' \
--data '{"title":"myTitle", "date": "2019-04-28T14:45:15", "comment": "cmt", "type": "bloodPressure", "user": "123a"}'
s
# patch measurement
curl --location --request PATCH 'http://localhost:3000/api/v1/measurement/659a89130ea326c42db23007' \
--header 'Content-Type: application/json' \
--data '{
    "title": "New Title",
    "date": "2023-04-28T14:45:15",
    "comment": "2NEW comment",
    "user": "xxx"
}'
```
