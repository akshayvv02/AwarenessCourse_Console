# Course Management Web Application - TrainerCentral API Integration

## Project Overview
This project involves developing a web application that enables users to:
1. **Bulk upload** a CSV file to invite learners to courses.
2. **Monitor real-time progress** of learners enrolled in the courses.

The web application is integrated with **TrainerCentral APIs** and supports secure user authentication, bulk operations, and real-time data fetching. The system is designed to ensure continuous operation with OAuth token management and Dockerized deployment.

---

## Technologies Used
- **Backend Framework**: Flask (Python)
- **Frontend**: HTML, CSS, JavaScript
- **Database**: MongoDB (for storing user data, roles, token metadata)
- **API Integration**: TrainerCentral APIs using OAuth 2.0
- **Containerization**: Docker (for seamless deployment and integration)
- **Task Automation**: Token management scripts, scheduled refreshes
- **Security**: Token storage in secure cache, encrypted tokens

---

## Key Features
1. **Bulk CSV Upload**: Users can upload a CSV file to invite multiple learners to a course at once.
2. **Real-time Progress Monitoring**: Users can monitor the real-time progress of learners within the courses.
3. **User Authentication and Role Management**: MongoDB is used to store users, including administrators, ensuring role-based access.
4. **OAuth Token Management**:
   - Uses **access tokens** and **refresh tokens** for secure API calls to TrainerCentral.
   - A **hybrid manual/automated approach** for refreshing tokens to ensure uptime and handle the 20-use refresh token limit.

---

## Project Workflow

### 1. OAuth Token Management
- **Token Set Generation**:
  - Seven sets of **access tokens** and **refresh tokens** are generated, providing 7 days of continuous operation.
  - These tokens are securely stored in the application server and refreshed manually by a maintenance team every Monday.

- **Automated Token Refresh**:
  - Each access token is valid for 60 minutes.
  - A background job checks token expiration and automatically refreshes the tokens using the associated refresh tokens until they reach their limit.
  
- **Manual Maintenance**:
  - After each set of refresh tokens reaches 18-19 uses, the maintenance team regenerates new tokens to ensure the application stays up for the next week.

### 2. Bulk CSV Upload
- Users can log into the system, upload a CSV file, and invite learners to courses in bulk using the TrainerCentral API.
- The CSV processing and API calls are managed using Flask and are processed asynchronously to ensure a smooth user experience.

### 3. Real-time Progress Monitoring
- Users can view the real-time progress of learners enrolled in courses.
- The application periodically calls the TrainerCentral API to fetch updated progress data and displays it dynamically on the web interface.

---

## System Architecture

### 1. **Frontend**:
   - Developed using **HTML, CSS, and JavaScript** to provide a user-friendly interface for users.
   - Provides features like CSV uploads, course invitations, and progress monitoring.

### 2. **Backend**:
   - **Flask**: The web application backend handles user authentication, CSV uploads, and communication with TrainerCentral APIs.
   - **MongoDB**: Used to store user information, token metadata, and logs of actions performed by users and administrators.

### 3. **OAuth Integration**:
   - **OAuth 2.0** authentication with TrainerCentral APIs.
   - **Offline access** is used to generate refresh tokens, and access tokens are refreshed as needed.
   - Seven token sets are used for continuous operation, and a hybrid approach is taken for manual and automated token refreshes.

### 4. **Token Security**:
   - Tokens are stored in a secure cache in the application server with encryption.
   - **Token rotation and invalidation** mechanisms are in place to ensure tokens are not misused.

---

## Docker Setup
- The entire application is **Dockerized** for seamless deployment and scalability.
- **Docker Compose** is used to integrate Flask, MongoDB, and other components.
- This setup ensures the application can be easily deployed across different environments.

---

## Improvements and Future Work
1. **Full Token Automation**: Automate the entire token refresh and regeneration process to remove the need for manual intervention.
2. **Scalability**: Introduce horizontal scaling to handle an increasing number of users and API requests.
3. **Improved API Handling**: Optimize the real-time progress monitoring using polling or webhooks to reduce API call frequency and improve performance.
4. **Error Handling**: Implement more robust error handling for OAuth token management and API rate limits.

---

## Conclusion
This project provides a secure, scalable, and user-friendly solution for users to manage course invitations and learner progress tracking. With OAuth token management, Dockerized deployment, and MongoDB for user management, it is designed for continuous and reliable operation.

