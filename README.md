# Buy Better Project

This is an entry point for Buy Better project. It contains the big picture of project.

## Overview
We are in an era of online shopping/ecommerce. Unfortunate, There are only 2 big ecommerce in my country to use. 
So I have a limited choice. The pain point here is the price showing is fluctuate between a days or weeks. 
Did I get the fair price ? Is it expensive or cheaper than yesterday or week ? The price showing in the application
is not reliable. No transparent or clear price information. Moreover, if you want to compare same item but difference 
ecommerce application. It's going to be a tedious task to do it manually 

What Buy Better is trying to do is let the user keep track the price for specific item. how was the price compare to 
last week, what is the lowest and highest price and when it occurs. set the notification when the price is below the 
threshold, compare the price between 2 sellers or application. etc. 

In conclusion Buy Better is an online shopping assistant. All you have to do is sent the product url 
and admin will set things up.

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
- [Buy-Better Admin UI](https://github.com/opplieam/bb-admin-ui) *Details implementation
- [Buy-Better Core API](https://github.com/opplieam/bb-core-api)
- [Buy-Better Core UIi](https://github.com/opplieam/bb-core-ui)
- [Buy-Better Centralized proto](https://github.com/opplieam/bb-grpc)
- [Buy-Better Product service](https://github.com/opplieam/bb-product-server)
- ~~[Buy-Better web scraping]~~  I take down the service due to the banning issue

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
This project should design as a `monolith` system design pattern because there is only 1 developer and cost of 
`microservice` will not pay off. 

BUT I make this project for the learning purpose. So I pick `distributed monolith` as a system design pattern
So it sit between `monolith` and `microservice`. Also, have a room to learn a new things.

The database system design pattern part is weired because I to find the halfway point of monolith and microservice
ends up with a questionable design. If I have to re-design, It should be like this
  * 1 database from the beginning until `Choreography pattern` is required (event driven) or learning `message queue`, 
then split database would be a good idea. 

## TO LEARN
- `Choreography design pattern`
- opentelemetry / observation
- Server Sent Event