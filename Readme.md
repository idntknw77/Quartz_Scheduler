# Spring Boot Quartz Scheduler Email Scheduling app


## Requirements

1. Java - 1.8.x

2. Maven - 3.x.x

3. MySQL - 5.x.x

## Steps to Setup

**1. Clone the application**

```bash
git clone https://github.com/callicoder/spring-boot-mysql-rest-api-tutorial.git
```

**2. Create MySQL database**

```bash
create database quartz_demo
```

**3. Change MySQL username and password as per your MySQL installation**

open `src/main/resources/application.properties`, and change `spring.datasource.username` and `spring.datasource.password` properties as per your mysql installation


**4. Setup Spring Mail**

The project is using Gmail's SMTP server for sending emails. Whether you use Gmail or any other SMTP server, you'll need to configure the following mail properties accordingly -

```properties
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=rajeevc217@gmail.com
spring.mail.password=
```

If you're using Gmail, you need to allow the third party apps to send emails by following the instructions below -

+ Go to https://myaccount.google.com/security?pli=1#connectedapps
+ Set ‘Allow less secure apps’ to YES

**5. Create Quartz Tables**

The project stores all the scheduled Jobs in MySQL database. You'll need to create the tables that Quartz uses to store Jobs and other job-related data. Please create Quartz specific tables by executing the `quartz_tables.sql` script located inside `src/main/resources` directory.

```bash
mysql> source <PATH_TO_QUARTZ_TABLES.sql>
```

**6. Build and run the app using maven**

Finally, You can run the app by typing the following command from the root directory of the project -

```bash
mvn spring-boot:run
```

# Scheduling an Email using the /scheduleEmail API

```bash
curl -i -H "Content-Type: application/json" -X POST \
-d '{"email":"callicoder@gmail.com","subject":"Test Mail","body":"Dear Future me, <br><br> <b>Think Big And Don’t Listen To People Who Tell You It Can’t Be Done. Life’s Too Short To Think Small.</b> <br><br> Cheers, <br>Prabhat!","dateTime":"2021-04-28T16:15:00","timeZone":"Asia/Kolkata"}' \
http://localhost:8080/scheduleEmail
http://localhost:8080/scheduleEmailEveryday    -- This will execute a task per minute as per the cron expresssion ("0 0/2 * 1/1 * ? *"). 
# Output
{"success":true,"jobId":"0741eafc-0627-446f-9eaf-26f5d6b29ec2","jobGroup":"email-jobs","message":"Email Scheduled Successfully!"}
```