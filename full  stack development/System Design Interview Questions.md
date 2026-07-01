# Low-Level Design (LLD) / System Design Interview Questions

> A comprehensive guide to mastering **Low-Level Design (LLD)** and **System Design** interviews from **Beginner → Intermediate → Advanced → FAANG/Staff Engineer** level.

---

# Table of Contents

* Introduction
* What is System Design?
* High-Level Design (HLD) vs Low-Level Design (LLD)
* Interview Roadmap
* Interview Process
* Core Computer Science Concepts
* Object-Oriented Programming
* SOLID Principles
* Design Principles
* Design Patterns
* UML Diagrams
* Database Design
* API Design
* Distributed Systems
* Scalability Concepts
* Concurrency
* Caching
* Microservices
* Cloud Architecture
* Security
* LLD Interview Questions
* HLD Interview Questions
* FAANG-Level Questions
* Real Company Questions
* Best Books
* Best Courses
* GitHub Repositories
* Practice Platforms
* Projects
* Interview Tips
* Resources

---

# Introduction

System Design interviews evaluate your ability to create scalable, maintainable, reliable, and efficient software systems.

There are generally two categories:

* High-Level Design (HLD)
* Low-Level Design (LLD)

Large technology companies such as Google, Amazon, Microsoft, Uber, Netflix, Meta, Apple, Airbnb, LinkedIn, Stripe, and many startups conduct one or both interviews.

---

# What is High-Level Design?

High-Level Design focuses on the architecture of the entire system.

It answers questions like

* How will millions of users access the application?
* How will servers communicate?
* Which database should be used?
* How can the system scale?
* How is data replicated?

Example

Design YouTube

Topics

* APIs
* Load Balancer
* CDN
* Cache
* Database
* Object Storage
* Message Queue
* Microservices
* Monitoring

---

# What is Low-Level Design?

LLD focuses on writing maintainable object-oriented software.

It answers

* What classes exist?
* What methods exist?
* Which Design Pattern should be used?
* How do objects interact?

Example

Design Parking Lot

You must create

* Classes
* Interfaces
* Relationships
* UML Diagram
* Design Patterns

---

# HLD vs LLD

| Feature         | HLD               | LLD                   |
| --------------- | ----------------- | --------------------- |
| Scope           | Entire System     | Individual Components |
| Focus           | Architecture      | Classes               |
| Scale           | Millions of users | Few objects           |
| Database        | Yes               | Optional              |
| APIs            | Yes               | Limited               |
| Design Patterns | Few               | Heavy usage           |
| OOP             | Basic             | Extensive             |
| UML             | Optional          | Required              |
| Coding          | No                | Yes                   |

---

# Interview Roadmap

## Stage 1

Programming

* Java
* C++
* Python
* JavaScript
* C#

---

## Stage 2

Data Structures

* Arrays
* Linked List
* Queue
* Stack
* Trees
* Graphs
* Heap
* HashMap

---

## Stage 3

Algorithms

* Sorting
* Searching
* Dynamic Programming
* Greedy
* Graph Algorithms

---

## Stage 4

Object-Oriented Programming

* Class
* Object
* Inheritance
* Abstraction
* Encapsulation
* Polymorphism

---

## Stage 5

SOLID Principles

* Single Responsibility
* Open Closed
* Liskov Substitution
* Interface Segregation
* Dependency Inversion

---

## Stage 6

Design Patterns

* Creational
* Structural
* Behavioral

---

## Stage 7

System Design

* LLD
* HLD

---

# Core Computer Science Topics

## Networking

* HTTP
* HTTPS
* TCP
* UDP
* DNS
* SSL
* TLS
* WebSocket
* REST
* GraphQL
* gRPC

---

## Operating System

* Process
* Thread
* Mutex
* Semaphore
* Scheduling
* Memory
* Deadlock

---

## Database

SQL

* MySQL
* PostgreSQL

NoSQL

* MongoDB
* Cassandra
* DynamoDB
* Redis

---

## Distributed Systems

* CAP Theorem
* Consistency
* Availability
* Partition Tolerance
* Replication
* Sharding
* Consensus
* Leader Election

---

# OOP Concepts

* Object
* Class
* Method
* Constructor
* Interface
* Abstract Class
* Encapsulation
* Abstraction
* Polymorphism
* Composition
* Aggregation
* Association
* Dependency

---

# SOLID Principles

## SRP

One class should have only one responsibility.

---

## OCP

Open for extension

Closed for modification

---

## LSP

Derived classes should replace base classes.

---

## ISP

No fat interfaces.

---

## DIP

Depend on abstractions.

---

# Design Patterns

## Creational

* Singleton
* Builder
* Factory
* Abstract Factory
* Prototype

---

## Structural

* Adapter
* Decorator
* Facade
* Composite
* Proxy
* Flyweight
* Bridge

---

## Behavioral

* Observer
* Strategy
* State
* Chain of Responsibility
* Command
* Mediator
* Iterator
* Visitor
* Memento
* Template Method

---

# UML Diagrams

* Class Diagram
* Sequence Diagram
* Activity Diagram
* State Diagram
* Object Diagram
* Component Diagram
* Deployment Diagram

---

# API Design

REST

* GET
* POST
* PUT
* PATCH
* DELETE

GraphQL

gRPC

Versioning

Authentication

Pagination

Rate Limiting

---

# Scalability Concepts

* Vertical Scaling
* Horizontal Scaling
* Load Balancing
* Auto Scaling
* CDN
* Cache
* Reverse Proxy
* Compression

---

# Caching

* Redis
* Memcached
* Local Cache
* Distributed Cache
* Cache Aside
* Write Through
* Write Back
* Read Through

---

# Message Queues

* Kafka
* RabbitMQ
* ActiveMQ
* Pulsar
* SQS

---

# Databases

SQL

* ACID
* Joins
* Indexing
* Transactions

NoSQL

* Eventual Consistency
* Partitioning

---

# Cloud

AWS

* EC2
* S3
* Lambda
* DynamoDB
* API Gateway
* CloudFront

Azure

Google Cloud

Kubernetes

Docker

---

# Monitoring

* Prometheus
* Grafana
* ELK
* Loki
* Jaeger
* Zipkin

---

# Logging

* Structured Logs
* Log Aggregation
* Log Rotation
* Error Monitoring

---

# Security

* JWT
* OAuth
* OpenID Connect
* API Keys
* RBAC
* HTTPS
* TLS
* Encryption
* Rate Limiting

---

# Low-Level Design Interview Questions

## Beginner

* Design ATM
* Design Elevator
* Design Library Management System
* Design Hotel Management
* Design Movie Ticket Booking
* Design Restaurant
* Design Student Management
* Design Employee Management
* Design Banking System
* Design Hospital

---

## Intermediate

* Design Parking Lot
* Design Chess
* Design Snake Game
* Design Tic Tac Toe
* Design Splitwise
* Design Cricbuzz
* Design Inventory System
* Design Cab Booking
* Design BookMyShow
* Design Shopping Cart

---

## Advanced

* Design WhatsApp
* Design Instagram
* Design Uber
* Design Netflix
* Design Spotify
* Design Slack
* Design Discord
* Design Airbnb
* Design Amazon
* Design Google Drive

---

## Expert

* Design Kubernetes Scheduler
* Design Distributed Cache
* Design Kafka
* Design Search Engine
* Design Database
* Design Git
* Design Docker
* Design Kubernetes
* Design Blockchain
* Design AI Agent Framework

---

# High-Level Design Interview Questions

## Storage

* Dropbox
* Google Drive
* OneDrive

---

## Streaming

* YouTube
* Netflix
* Spotify

---

## Social Media

* Facebook
* Instagram
* Twitter
* LinkedIn

---

## Communication

* WhatsApp
* Slack
* Discord
* Zoom

---

## E-commerce

* Amazon
* Flipkart
* Shopify

---

## Transportation

* Uber
* Ola
* Lyft

---

## Finance

* PayPal
* Stripe
* UPI
* Banking

---

## Search

* Google Search
* Elasticsearch

---

## Maps

* Google Maps
* Uber Maps

---

## AI

* ChatGPT
* AI Coding Assistant
* AI Search Engine
* AI Agent Platform

---

# FAANG Interview Questions

## Google

* Google Docs
* Gmail
* Google Photos
* Google Calendar
* BigTable
* Google Search

---

## Amazon

* Amazon Cart
* Amazon Prime
* DynamoDB
* Kindle

---

## Meta

* Messenger
* Instagram Feed
* Facebook Timeline
* Reels

---

## Netflix

* Recommendation Engine
* Streaming Service

---

## Uber

* Uber Driver Matching
* ETA Calculation

---

# Common LLD Questions

* Design Cache
* Design Logger
* Design Notification Service
* Design File System
* Design URL Shortener
* Design Text Editor
* Design Music Player
* Design Calendar
* Design Voting System
* Design Chat Application
* Design Email Service
* Design Gaming Engine

---

# Real Interview Questions

### Easy

* ATM
* Library
* Hotel
* Bank
* Calendar

### Medium

* Parking Lot
* Chess
* Splitwise
* Cricbuzz
* BookMyShow

### Hard

* WhatsApp
* Uber
* Netflix
* YouTube
* Twitter

---

# Books

## LLD

* Head First Design Patterns
* Clean Code
* Clean Architecture
* Agile Software Development
* Refactoring
* Domain-Driven Design

---

## HLD

* Designing Data Intensive Applications
* System Design Interview Volume 1
* System Design Interview Volume 2
* Building Microservices
* Release It

---

# GitHub Resources

* Awesome System Design
* System Design Primer
* Awesome Scalability
* Awesome Distributed Systems
* Awesome Design Patterns

---

# YouTube Channels

* Gaurav Sen
* Jordan has no life
* Arpit Bhayani
* ByteByteGo
* Hussein Nasser
* Tech Dummies
* CodeKarle

---

# Practice Platforms

* LeetCode
* InterviewBit
* GeeksforGeeks
* Design Gurus
* Exponent
* Educative
* Pramp

---

# Hands-on Projects

* URL Shortener
* Distributed Cache
* Chat Application
* Food Delivery
* E-Commerce
* Video Streaming
* Banking System
* Ride Sharing
* Notification System
* Online Judge
* AI Chatbot

---

# Interview Tips

* Clarify requirements.
* Identify functional and non-functional requirements.
* Draw diagrams.
* Think aloud.
* Discuss trade-offs.
* Consider scalability.
* Handle failures.
* Design APIs.
* Optimize databases.
* Explain bottlenecks.
* Write clean code.
* Follow SOLID principles.
* Use appropriate Design Patterns.
* Test edge cases.
* Discuss future improvements.

---

# 90-Day Preparation Plan

### Month 1

* OOP
* SOLID
* Design Patterns
* UML
* LLD Problems

### Month 2

* Distributed Systems
* Databases
* Networking
* Scalability
* APIs

### Month 3

* HLD Problems
* Mock Interviews
* Company-Specific Questions
* End-to-End Projects

---

# Final Checklist

* ✅ Object-Oriented Programming
* ✅ SOLID Principles
* ✅ Design Patterns
* ✅ UML Diagrams
* ✅ Clean Code
* ✅ Refactoring
* ✅ Database Design
* ✅ API Design
* ✅ Distributed Systems
* ✅ Scalability
* ✅ Caching
* ✅ Concurrency
* ✅ Message Queues
* ✅ Cloud Fundamentals
* ✅ Security
* ✅ Microservices
* ✅ Monitoring
* ✅ Logging
* ✅ Real Interview Questions
* ✅ Mock Interviews
* ✅ Hands-on Projects

---

# Repository Structure (Recommended)

```text
System-Design/
│
├── README.md
├── Low-Level-Design/
│   ├── OOP
│   ├── SOLID
│   ├── Design Patterns
│   ├── UML
│   ├── Interview Questions
│   └── Projects
│
├── High-Level-Design/
│   ├── Scalability
│   ├── Databases
│   ├── Caching
│   ├── Networking
│   ├── Distributed Systems
│   ├── Microservices
│   ├── Case Studies
│   └── Interview Questions
│
├── Company-Wise/
│   ├── Google
│   ├── Amazon
│   ├── Microsoft
│   ├── Meta
│   ├── Uber
│   ├── Netflix
│   └── Airbnb
│
├── Mock Interviews
├── Projects
├── Resources
└── Notes
```

---

# Goal

By completing this roadmap and practicing the interview questions, you will be prepared for:

* FAANG System Design Interviews
* Startup Engineering Interviews
* Senior Software Engineer Roles
* Staff Engineer Roles
* Principal Engineer Roles
* Software Architect Positions
* Tech Lead Interviews

This README can serve as the foundation for a complete **System Design Interview** repository, organizing learning materials, notes, code examples, diagrams, and solutions in one place.
