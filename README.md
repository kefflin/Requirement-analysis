# Requirement Analysis in Software Development

Welcome to the **Requirement Analysis** repository. This repository is dedicated to documenting and managing the process of requirement analysis in software development projects.

Requirement analysis is a critical phase in the Software Development Life Cycle (SDLC) that involves gathering, analyzing, validating, and documenting the needs and expectations of stakeholders. The purpose of this repository is to provide structured documentation, templates, and guidelines that ensure clear communication between clients, developers, and project managers.

Whether you're working on a small application or a large enterprise system, this repository will help you define functional and non-functional requirements, maintain traceability, and avoid common pitfalls that arise from poorly defined project scopes.

# What is Requirement Analysis?

Requirement Analysis is a fundamental phase in the Software Development Life Cycle (SDLC) where the needs, expectations, and constraints of stakeholders are gathered, analyzed, and documented to define the scope of a software project. This process ensures that the development team fully understands what the end-users and clients expect from the software system before any design or coding begins.

Key Activities in Requirement Analysis:
Requirement Gathering: Collecting information from stakeholders through interviews, surveys, observations, and documentation.

Requirement Elicitation: Engaging stakeholders to uncover implicit needs and expectations that may not be immediately obvious.

Requirement Documentation: Organizing and recording requirements in structured formats such as Software Requirements Specification (SRS) documents, user stories, or use cases.

Requirement Validation: Ensuring that the gathered requirements are accurate, complete, feasible, and aligned with business objectives.

Requirement Management: Maintaining and tracking requirements throughout the project lifecycle to handle changes and ensure traceability.

Importance of Requirement Analysis in SDLC:
Foundation for Development: Clearly defined requirements provide a solid foundation for system design, development, and testing.

Minimizes Project Risks: Helps in identifying potential conflicts, ambiguities, or unrealistic expectations early in the process.

Improves Communication: Acts as a reference point that aligns the understanding of clients, developers, testers, and project managers.

Cost and Time Efficiency: Well-analyzed requirements reduce rework, project delays, and cost overruns caused by scope creep or misunderstood requirements.

Enhances Product Quality: Ensures that the final software product meets user needs and performs as expected in its intended environment.

Effective requirement analysis bridges the gap between what stakeholders expect and what developers deliver, making it a critical success factor for any software project.

# Why is Requirement Analysis Important?

Requirement Analysis plays a pivotal role in the success of software development projects. It lays the groundwork for the entire Software Development Life Cycle (SDLC) by ensuring that all stakeholders share a clear and common understanding of what the software is expected to achieve. Below are three key reasons why Requirement Analysis is critical:

1. Prevents Miscommunication and Misunderstandings
Requirement Analysis establishes a clear line of communication between stakeholders, including clients, project managers, developers, and testers. By documenting explicit and detailed requirements, it minimizes assumptions and ambiguities, ensuring everyone is aligned on the project’s objectives.

2. Reduces Cost and Time Overruns
Identifying and addressing requirements early in the SDLC helps avoid costly changes and rework during later stages of development. A thorough requirement analysis reduces the chances of scope creep, project delays, and budget overruns by setting clear expectations from the outset.

3. Ensures Delivery of Quality Software Solutions
A well-defined set of requirements ensures that the final product meets the user’s needs and performs reliably in real-world scenarios. Requirement Analysis contributes to building software that aligns with business goals, enhances user satisfaction, and complies with technical and regulatory standards.

# Key Activities in Requirement Analysis

Requirement Analysis involves several critical activities that help ensure a clear understanding of what the software should achieve. The five key activities are:

.Requirement Gathering:

  .Involves collecting information about the needs and expectations of stakeholders (clients, users, management).

  .Techniques include interviews, questionnaires, workshops, observations, and reviewing existing documentation.

.Requirement Elicitation:

  .Focuses on uncovering implicit, hidden, or unclear needs that stakeholders may not express directly.

  .Involves brainstorming sessions, prototyping, use case development, and scenario analysis to explore user needs in depth.

.Requirement Documentation:

  .Captures and organizes all gathered requirements in a structured format.

  .Common documentation includes Software Requirements Specification (SRS), User Stories, Use Cases, and Requirement Traceability        Matrices (RTM).

.Requirement Analysis and Modeling:

  .Involves analyzing gathered requirements to detect conflicts, redundancies, or gaps.

  .Uses visual models like Data Flow Diagrams (DFD), Entity-Relationship Diagrams (ERD), and Unified Modeling Language (UML) diagrams    to represent system requirements.

.Requirement Validation:

  .Ensures that the documented requirements are correct, complete, feasible, and aligned with stakeholder expectations.

  .Activities include requirement reviews, walkthroughs, and formal approval from stakeholders to verify accuracy and acceptance.
  
# Types of Requirements.

In software development, requirements are generally classified into Functional Requirements and Non-functional Requirements. Understanding the distinction between the two is essential for building a system that not only performs its intended tasks but also meets quality standards.

#Functional Requirements
Functional Requirements define what the system should do. They describe the specific behaviors, features, and functions that the software must support to meet the business objectives.

Definition:
Functional Requirements specify the system's functional aspects, outlining the tasks, data handling, and operations the system must perform.

Examples for a Booking Management Project:
The system shall allow users to create, modify, and cancel bookings.

The system shall send booking confirmation emails to users upon successful reservation.

The admin shall be able to view and manage all booking records from a centralized dashboard.

The system shall allow users to filter available booking slots by date, time, and location.

The system shall automatically update availability when a booking is confirmed or cancelled.

Non-functional Requirements
Non-functional Requirements define how the system should perform. They describe the quality attributes of the system, such as performance, security, usability, and scalability.

Definition:
Non-functional Requirements specify the system's operational characteristics, setting constraints and standards for how the system functions rather than what it does.

Examples for a Booking Management Project:
The system shall be able to handle up to 1,000 concurrent booking requests without performance degradation.

The system shall ensure all user data is encrypted both in transit and at rest.

The system shall have an uptime availability of 99.9% per month.

The booking interface shall load within 3 seconds on mobile and desktop devices.

The system shall support multi-language interfaces, including English and Swahili.

The system shall comply with GDPR and local data protection regulations.
Let’s understand the flow one by one. I have divided it into 3 parts:

Hotel Management Service
Customer Service (Search + Booking)
View Booking Service
Final Design
Hotel Management Service
This is the service that will be given to hotel managers/owners. In this managers can manage their hotel's related information. Here managers have a separate portal to access the data and update it.

Zoom image will be displayed

Hotel Management Service Architecture
Whenever an API is triggered from the hotel manager app the initial request is been sent to the load balancer, then the load balancer distributes the requests to the desired server to process. The hotel service cluster has multiple servers that have the container for hotel service-related API.

Now, this hotel service interacts with the Hotel DB cluster which follows the master-slave architecture to reduce the load in the database. Basically, in this approach, we create a replica of the master database which are called a slave database. Master DB is used for a write operation and slave DB is used for reading operation only. Whenever a write operation is performed on the master database it syncs the data to the slave database.

Whenever any data is updated in the database API sends the data to the CDN(Content Distributed Network) and to a Messaging Queue System(like Kafka, RabbitMQ) for further processing. A CDN is a geographically distributed group of servers that work together to provide fast delivery of Internet content.

Customer Service (Search + Booking)
This is the service that will be given to customers. In this customers can search and book a hotel. Here customers have a separate portal to access the data and process it.

Zoom image will be displayed

Customer Service Architecture
The CDN app shows the content to customers like the nearby hotels, recommendations, offers etc.

As we discussed in the previous section, hotel data is sent to messaging queue system to process it. Here we have a messaging queue consumer that takes the data from the queue and stores the data in elastic search.

The customer app hit’s the API then the load balancer redirect and distribute the request to the respective service to process the request. Here we have two services one for searching for a hotel and a booking service to book the hotel and booking service also interacts with the payment service which will be a third-party service.

The search service has to get the data from Elastic Search. Elasticsearch is a NoSQL Database that is best for its search engine functionality.

The booking service communicates with Redis and the booking database cluster. Redis is caching system, that’s stores temporary data so that data need not fetched database and which could eventually reduce the load in the database also reduce the response time of API.

Any changes made in the database will be sent to the messaging queue. Then the consumer will take the data from the queue and put it to Casandra. For archival we are using Casandra because with time data size will increase in the database, increasing query time. So that’s why we may need to delete old data from the database. And Casandra is a NoSQL database that is good at handling a high volume of data.

View Booking Service
Here all current and old booking details are shown to the user. Both managers and customers use this service.

Zoom image will be displayed

View Booking Architecture
The Customer/Manager app sends the request to the load balancer and it distributes the request to booking management servers. Then the service request for data through Redis and Cassandra. through Redis, it requests recent data as it is a caching server. Which could reduce the loading time on the app side.

Final Design
Zoom image will be displayed

Hotel Booking System Design
As you can see in the above design there is a Kafka consumer for notification, notification consumers send the notification. That could be to the customer/manager, like whenever a customer books a hotel notification is sent to the manager or if a new offers come it’s notified to the customer.

Apache Streaming service takes the data from messaging queue and stores it in Hadoop which could be used for BigData analysis for multiple purposes. Like business analysis, finding potential customers, audience categorisations etc.
  
