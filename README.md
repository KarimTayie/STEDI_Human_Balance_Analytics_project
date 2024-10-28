# Project: STEDI Human Balance Analytics

## Introduction

Spark and AWS Glue allow you to process data from multiple sources, categorize the data, and curate it to be queried in the future for multiple purposes. As a data engineer on the STEDI Step Trainer team, you'll need to extract the data produced by the STEDI Step Trainer sensors and the mobile app, and curate them into a data lakehouse solution on AWS so that Data Scientists can train the learning model. 

## Project Details

The STEDI Team has been hard at work developing a hardware STEDI Step Trainer that:

- trains the user to do a STEDI balance exercise;
- and has sensors on the device that collect data to train a machine-learning algorithm to detect steps;
- has a companion mobile app that collects customer data and interacts with the device sensors.

STEDI has heard from millions of early adopters who are willing to purchase the STEDI Step Trainers and use them.

Several customers have already received their Step Trainers, installed the mobile application, and begun using them together to test their balance. The Step Trainer is just a motion sensor that records the distance of the object detected. The app uses a mobile phone accelerometer to detect motion in the X, Y, and Z directions.

The STEDI team wants to use the motion sensor data to train a machine learning model to detect steps accurately in real-time. Privacy will be a primary consideration in deciding what data can be used.

Some of the early adopters have agreed to share their data for research purposes. Only these customers’ Step Trainer and accelerometer data should be used in the training data for the machine learning model.

## Implementation

### Landing Zone

**Glue Tables**:

- [customer_landing.sql](ddls/customer_landing.sql)
- [accelerometer_landing.sql](ddls/accelerometer_landing.sql)
- [step_trainer_landing.sql](ddls/step_trainer_landing.sql)

**Athena**:
Landing Zone data query results

*Customer Landing*:

<figure>
  <img src="screenshots/landing/customer_landing_count.png" alt="Customer Landing Count" width=60% height=60%>
</figure>

<figure>
  <img src="screenshots/landing/customer_landing_non_null_count.png" alt="Customer Landing Non Null Count" width=60% height=60%>
</figure>

*Accelerometer Landing*:

<figure>
  <img src="screenshots/landing/accelerometer_landing_count.png" alt="Accelerometer Landing Count" width=60% height=60%>
</figure>

*Step Trainer Landing*:

<figure>
  <img src="screenshots/landing/step_trainer_landing_count.png" alt="Step Trainer Landing Count" width=60% height=60%>
</figure>

### Trusted Zone

**Glue job scripts**:

- [customer_landing_to_trusted.py](glue_jobs/customer_landing_to_trusted.py)
- [accelerometer_landing_to_trusted_zone.py](glue_jobs/accelerometer_landing_to_trusted.py)
- [step_trainer_trusted_zone.py](glue_jobs/step_trainer_trusted.py)

**Athena**:
Trusted Zone Query results:

*Customer Trusted*:

<figure>
  <img src="screenshots/trusted/customer_trusted_count.png" alt="Customer Trusted Count" width=60% height=60%>
</figure>

<figure>
  <img src="screenshots/trusted/customer_trusted_non_null_count.png" alt="Customer Trusted Non Null Count" width=60% height=60%>
</figure>

*Accelerometer Trusted*:

<figure>
  <img src="screenshots/trusted/accelerometer_trusted_count.png" alt="Accelerometer Trusted Count" width=60% height=60%>
</figure>

*Step Trainer Trusted*:

<figure>
  <img src="screenshots/trusted/step_trainer_trusted_count.png" alt="Step Trainer Trusted Count" width=60% height=60%>
</figure>

### Curated Zone

**Glue job scripts**:

- [customer_trusted_to_curated.py](glue_jobs/customer_trusted_to_curated.py)
- [machine_learning_curated.py](glue_jobs/machine_learning_curated.py)

**Athena**:
Curated Zone Query results:

*Customer Curated*:

<figure>
  <img src="screenshots/curated/customer_curated_count.png" alt="Customer Curated Count" width=60% height=60%>
</figure>

*Machine Learning Curated*:

<figure>
  <img src="screenshots/curated/machine_learning_curated_count.png" alt="Machine Learning Curated Count" width=60% height=60%>
</figure>
