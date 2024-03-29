# ReactJS Weather App with Jenkins and Docker

This project demonstrates how to build and deploy a ReactJS weather app using Jenkins and Docker.

## Prerequisites

- Node.js
- Docker
- Jenkins (configured with necessary plugins)

## Setup

1. **Clone Repository:**

   - Clone this repository and delete the `.env.enc` file from the project folder.

2. **Configure Jenkins Pipeline:**

   - Follow the instructions provided in the [Jenkins Installation Guide](https://github.com/Dev-Pradeep-NS/Documentation/tree/main/Jenkins-Installation).
   - Refer to [this guide](https://github.com/Dev-Pradeep-NS/Documentation/tree/main/SSH%20setup%20btw%20Jenkins%20and%20Github) for detailed steps on setting up SSH Authentication between GitHub and Jenkins.
   - Go to your Jenkins dashboard:
     - Click on **New Item** to create a new project.
     - Choose **Multibranch Pipeline** and click **OK**.
     - Give some Display name for your project.
     - In the Branch Sources section, Click on add resource dropdown and select single repository and branch.
     - Give some name and paste your GitHub repository URL in the **Repository URL** field and also you can specify the branch as well.
     - Apply and save the configuration.

3. **Create Encrypted `.env` File:**

   - Generate an encrypted `.env.enc` file containing your environment variables using the following command:
     ```
     openssl enc -aes-256-cbc -in .env -out .env.enc2 -pbkdf2
     ```

4. **Set up Docker Hub Credentials in Jenkins:**

   - Go to your Jenkins dashboard and click on **Manage Jenkins**.
   - Navigate to **Configure System**.
   - Scroll down to the **Global properties** section and check the box for **Environment variables**.
   - Define the following environment variables:
     - `APP_NAME`: weatherapp
     - `DOCKER_PASS`: docker_hub_password
     - `DOCKER_USER`: docker_hub_username
     - `ENV_PASSWORD`: password_used_to_encrypt .env file

5. **Build and Push Docker Image:**
   - The pipeline will build and push the Docker image to your Docker Hub registry.

## Environment Variables

To run this project, you will need to add the following environment variables to your `.env` file in the ReactJS application:

- `REACT_APP_WEATHER_KEY`: open_weather_api_key

## Dockerfile

The Dockerfile sets up a Node.js environment and installs dependencies.

## Jenkins Pipeline

If you want jenkins pipeline trigger automatically and build when you push code to github, you can refer [this guide](https://github.com/Dev-Pradeep-NS/Documentation/tree/main/Setting%20up%20webhooks%20for%20jenkins%20pipeline%20to%20trigger%20automatically) to make that happen.

## Usage

1. Run the Jenkins pipeline.
2. Access your ReactJS weather app via the Docker container.
