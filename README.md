# Buy Better Project

This is an entry point for Buy Better project. It contains the big picture of project.

Looking for the source code ? Please visit [List of all repositories](#list-of-services)

## Table of contents
- [Overview](#overview)
- [Overall Architect](#overall-architect)
- [List of all repositories](#list-of-services)
- [Overall database diagrams](#overall-database-diagrams)
- [Overall Tech stack](#overall-tech-stack)
- [Design choice](#design-choice)
- [To Learn List](#to-learn)

## Overview
We are currently in an era of online shopping and ecommerce. Unfortunately, there are only 2 major ecommerce platforms 
available in my country. This limits my options. The issue here is that the prices of products fluctuate from day to day 
or week to week. I find it difficult to determine if I am getting a fair price, and I can't tell if a product is more 
expensive or cheaper than it was yesterday or last week. The prices shown in the application are not reliable, 
and there is no transparent or clear pricing information. Additionally, comparing the same item across different 
ecommerce applications is a tedious task to do manually.

Buy Better aims to help users track the price of specific items. It allows users to compare the current price with 
the price from last week, identify the lowest and highest prices, and when they occurred. Users can also set 
notifications for when the price falls below a certain threshold, and compare prices between different sellers or 
applications.

In conclusion, Buy Better is an online shopping assistant. All you have to do is send the product URL, 
and the admin will set things up.

`NOTE: This project is for learning purpose and not fully complete yet`

## Overall architect
![architect](https://github.com/opplieam/buy-better/blob/main/diagram.drawio.png?raw=true)
This is not a final design.

There are 3 big parts.
1. Web scraping service
To keep up-to-date price. Web scraping is mandatory to do automate task. collecting price from target website
2. Buy Better Admin
The management from users to manually matching products / category (which I design the system to collect the data and 
prepare dataset at the same time for using in machine learning model in the future. So when the new category/item 
being scraped, it will automatically match to the existing system)
3. Buy Better Core
This part is where the user interact for both frontend and backend. I design to be the scalable, I will talk later
in the design choice section.

## List of services
- [Buy-Better Admin Backend](https://github.com/opplieam/bb-admin-api) *Details implementation
- [Buy-Better Admin Frontend](https://github.com/opplieam/bb-admin-ui) *Details implementation
- [Buy-Better Core Backend](https://github.com/opplieam/bb-core-api)
- [Buy-Better Core Frontend](https://github.com/opplieam/bb-core-ui)
- [Buy-Better Centralized proto/gRPC](https://github.com/opplieam/bb-grpc)
- [Buy-Better Product Service Backend](https://github.com/opplieam/bb-product-server)
- ~~[Buy-Better web scraping]~~ I take down the service due to the banning issue

## Overall database diagrams
![db-admin](https://github.com/opplieam/bb-admin-api/raw/main/Buy-Better-Admin.png?raw=true)
![dbcore](https://github.com/opplieam/bb-core-api/blob/main/Buy-Better-Core.png?raw=true)
This is not a final design.

## Overall Tech stack
### Web scraping
- Python
  * Scrapy / Splash
  * Playwright
### Frontend
- Typescript
  * React
    * React-query
    * Mantine
    * React-router
  * Playwright
  * Swagger UI
### Infrastructure
- Docker / docker-compose
- k8s
  * kustomize
  * minikube
  * bitnami seal secrets
### Backend
- Go
  * gin
  * paseto
  * testify
  * jet-db
  * dockertest
  * goth (Oauth)
- go-migrate
- mockery
- proto / GRPC
- openapi v3 
- postgres db

## Design choice
This project should be designed as a `monolith` system design pattern because there is only 1 developer, 
and the cost of a `microservice` will not pay off. However, since I am building this project for learning purposes, 
I have chosen to implement a `distributed monolith` as a system design pattern. 
This approach sits between a `monolith` and a `microservice`.

The database system design pattern part is confusing because I want to find a balance between a `monolithic` 
and `microservice` approach. It resulted in a questionable design. If I were to redesign it, I would do it like this:

* Start with one database until the `Choreography pattern` is required (event-driven), 
then splitting the database would be a good idea.

## TO LEARN
- `Choreography design pattern`
- opentelemetry / observation
- Server Sent Event