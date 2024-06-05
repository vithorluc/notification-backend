# Notification System

## Overview

This project is a notification system that categorizes messages into Sports, Finance, and Movies. It supports three types of notifications: SMS, Email, and Push Notification. Notifications are logged in a database but not actually sent.

## Project Structure

```
my-app/
├── Dockerfile
├── docker-compose.yml
├── .dockerignore
├── .env
├── ormconfig.json
├── package.json
├── package-lock.json
├── src/
│   ├── app.ts
│   ├── entity/
│   │   ├── Category.ts
│   │   ├── NotificationLog.ts
│   │   ├── NotificationType.ts
│   │   ├── User.ts
│   │   ├── UserNotificationChannel.ts
│   │   └── UserSubscription.ts
│   └── ...
└── README.md
```

## Database Tables

### Users

| Column      | Type    | Description         |
| ----------- | ------- | ------------------- |
| id          | INT     | Primary Key         |
| name        | VARCHAR | User's name         |
| email       | VARCHAR | User's email        |
| phoneNumber | VARCHAR | User's phone number |

### Categories

| Column | Type    | Description   |
| ------ | ------- | ------------- |
| id     | INT     | Primary Key   |
| name   | VARCHAR | Category name |

### NotificationTypes

| Column | Type    | Description            |
| ------ | ------- | ---------------------- |
| id     | INT     | Primary Key            |
| name   | VARCHAR | Notification type name |

### UserSubscriptions

| Column     | Type | Description               |
| ---------- | ---- | ------------------------- |
| id         | INT  | Primary Key               |
| userId     | INT  | Foreign Key to Users      |
| categoryId | INT  | Foreign Key to Categories |

### UserNotificationChannels

| Column             | Type | Description                      |
| ------------------ | ---- | -------------------------------- |
| id                 | INT  | Primary Key                      |
| userId             | INT  | Foreign Key to Users             |
| notificationTypeId | INT  | Foreign Key to NotificationTypes |

### NotificationLogs

| Column             | Type      | Description                      |
| ------------------ | --------- | -------------------------------- |
| id                 | INT       | Primary Key                      |
| userId             | INT       | Foreign Key to Users             |
| categoryId         | INT       | Foreign Key to Categories        |
| notificationTypeId | INT       | Foreign Key to NotificationTypes |
| message            | TEXT      | Notification message             |
| timestamp          | TIMESTAMP | Time of notification             |

## Environment Variables

Create a `.env` file in the root directory and add the following environment variables:

```
# Redis configuration
REDIS_HOST=redis
REDIS_PORT=6379

# MySQL configuration
MYSQL_HOST=mysql
MYSQL_PORT=3306
MYSQL_USER=root
MYSQL_PASSWORD=rootpassword
MYSQL_DATABASE=notifications
```

## Commands

### Build and Run the Project

To build and run the project using Docker Compose:

```sh
docker-compose up --build
```

### Install Dependencies

To install project dependencies:

```sh
npm install
```

### TypeORM Commands

To run TypeORM commands, use:

```sh
npx typeorm <command>
```

For example, to synchronize the database schema:

```sh
npx typeorm schema:sync
```

## Usage

### Starting the Application

After running `docker-compose up --build`, the application will be accessible at `http://localhost:3000`.

### Sending a Notification

To queue a notification, make a POST request to `/send-notification` with a JSON body containing `message`, `category`, and `userId`. Example using `curl`:

```sh
curl -X POST http://localhost:3000/send-notification -H "Content-Type: application/json" -d '{
  "message": "Your message here",
  "category": "Sports",
  "userId": 1
}'
```

## License

This project is licensed under the MIT License.

---

This README provides a clear structure for understanding, setting up, and running the project, including database details, environment configuration, and usage instructions.
