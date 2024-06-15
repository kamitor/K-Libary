## Last Sprint

#### What Went Well

1. **Ontology Implementation**: The ontology framework was successfully integrated, allowing the system to interpret and represent complex data structures. This approach replaces traditional relational database structures, enhancing the system's understanding and extensibility.

2. **Functionality Development**: Significant progress was made in developing the supply chain mapping feature. The ontology-based approach enables the system to guess nodes using first-order logic and automate the search process.

3. **AI Segmentation**: The process was effectively divided into three distinct AI components:
- AI for searching information.
- AI for making connections and data mashing.
- AI for creating displays, widgets, and tables.

4. **Feature Requests Addressed**: Important feature requests were noted and planned, such as the accuracy counter for supply chain mapping, which will indicate the confidence level of the mappings.

5. **Initial MVP**: An initial version of a minimally viable product (MVP) was demonstrated, showcasing the system's capabilities and its potential for real-world applications.

#### What Could Be Improved

1. **Accuracy and Quality Assurance**: Ensuring the system's accuracy is critical. There were concerns about the system providing correct answers but potentially missing small, vital components. A feature to address accuracy was requested.

2. **Focus and Scope Management**: It was emphasized to avoid getting into "rabbit holes" and attempting to perfect every aspect. The focus should be on achieving a functional product that provides reasonably accurate mappings.

3. **Balancing Development Efforts**: The need to balance efforts between creating a usable product and maintaining high accuracy was highlighted. It was noted that achieving a perfect solution might not be feasible in the short term.

#### Action Items for Next Sprint

1. **Accuracy Counter Development**: Implement the requested feature to provide an accuracy counter for supply chain mappings, helping users gauge the reliability of the system's outputs.

2. **Metric Integration**: Build metrics into the pipeline to assess the efficiency and impact of the fine-tunes on the system. This will help in evaluating performance and making necessary adjustments.

3. **User Feedback Integration**: Continue integrating user feedback to improve the system iteratively. Ensure that the MVP is usable and addresses the core needs of the users.

4. **Documentation and Training**: Provide clear documentation and training materials to help users understand and leverage the system effectively.

5. **Progress Monitoring**: Establish clear milestones for the next version of the MVP, ensuring it meets the defined criteria for usability and accuracy.

## Work done
- [x] create a protocol to allow the ai to control the UI elements and dynamically render various visualisations.
- [x]  CREWS need to start working; So that it can start crawling the internet for subquestions: "So it can say: Ah I need more information, go and search the internet".
- [x] Finetune: protocol to allow the ai to control the UI elements and dynamically render various visualisations
- [x] create an ontology to describe the supply chanin elements as a schema to help the AI structurize knowledge in a well defined way.
- [x] Chat system needs to work and update map upon prompt
- [x] Creating a digital environment and bringint it online. INFRASTUCTURE
## Work unfinished


- [ ] Ask multipule A.I's and Multipule Prompts, to identify the which of the data is correct.
- [ ] [in progress] Need to build the task scheduler for the A.I Crews - >  so that you can see what tasks are running and what is going on. So you can see it "Build" Data.
- [ ] Visual updates about the crews in the interface, so that we  can see what is running.

- [ ] [in progress] Load significantly more data into the model to parse
- [ ] [in progress]: Built an initial dataset to train AI models, improving accuracy from 40% to 70%.
- [ ] First version of the Application online
- [ ] Updating the Contacts sheet, making it into markdown so that everyone can read ORGANISATION

- [ ] Setup of Linkedin Page, LEGITEMACY
- [ ] Texten voor studenten, onboarding process for students. RECRUITMENT
- [ ] Organisation Starting: Creation of a B.V or Non-Profit? LEGITEMACY
- [ ] Setup Recruitment process for students, CRM. RECRUITMENT
- [ ] Creation of Online content for students to learn, LMS
- [ ] Filing for Public Grants, FUNDING
- [ ] Going to Several Events on behalf of Value Chain Hackers, NETWORKING
- [ ] Setup of Social Media for Value Chain Hackers, OUTREACH
- [ ] Making a website , Getting a domain, INFRASTRUCTURE
- [ ] Server Setup and config budget for Production. INFRASTUCTURE
- [ ] Setup Scripts
- [ ] Splitting the minds over multipule machines

## Next Sprint

## Tasks


Next Steps:

EPIC Visualize Power Dynamics Ecosystem: For the upcoming demo, develop a feature to visualize the entire ecosystem based on a company name within 20 minutes. 

#### Sprint 1: Basic Ontology Setup and Initial Data Integration

**Sprint Goal A**: Establish the foundation for the Power Dynamics Ecosystem visualization.

In order to do this: we need to build the ontology first; ontology to describe the supply chanin elements as a schema to help the AI structurize knowledge in a well defined way.
##### Sub-Goals A:

Define Key Supply Chain Elements:
Identify and document the primary elements such as suppliers, manufacturers, distributors, retailers, and consumers.
Define the relationships between these elements, including material flow, information flow, and financial flow.

**Sub-tasks**:

1. **Define Key Supply Chain Elements**:
    - Identify and document the primary elements such as suppliers, manufacturers, distributors, retailers, and consumers.
    - Define the relationships between these elements, including material flow, information flow, and financial flow.
2. **Develop Basic Schema**:
    - Create an initial schema using an ontology editor like Protégé to represent the supply chain elements and their relationships.
    - Ensure the schema is extensible for future updates.
3. **Test the Ontology with Sample Data**:
    - Use a small dataset to validate the ontology's structure and its ability to represent supply chain relationships accurately.
4. **Initial Data Integration**:
    - Collect a small, representative dataset and integrate it into the ontology with RDF4J.
    - Develop SPARQL queries to test the ontology and ensure it returns accurate and relevant results.


### Sprint Goal

To integrate all core components, ensure system reliability and accuracy, and prepare for a visual launch of the Power Dynamics Ecosystem feature.

### Sub-Goals

1. **Enhance Ontology Framework**: Finalize the ontology to ensure comprehensive and accurate representation of supply chain elements and relationships.
2. **Develop and Refine Visualizations**: Create intuitive and dynamic visualizations to display supply chain mappings and power dynamics.
3. **User Feedback Integration**: Collect and integrate feedback from initial users to improve system usability and functionality.
4. **System Testing and Quality Assurance**: Conduct thorough testing to ensure the accuracy and reliability of the system's outputs.
5. **Prepare for Visual Launch**: Finalize all elements required for a successful visual launch, including documentation, marketing materials, and a demo.

### Sub-Goals and Optional Tasks

#### Sub-Goal 1: Enhance Ontology Framework
1. **Refine Schema**:
    - [ ] Review and update the initial schema based on feedback and testing.
    - [ ] Ensure the schema covers all key supply chain elements and their relationships comprehensively.
    - [ ] **Optional Task**: Conduct workshops with domain experts to validate the schema.

2. **Expand Data Integration**:
    - [ ] Integrate additional datasets to enrich the ontology.
    - [ ] Test the system with larger datasets to validate scalability and performance.
    - [ ] **Optional Task**: Develop automated data integration pipelines.

#### Sub-Goal 2: Develop and Refine Visualizations
1. **Design Visual Elements**:
    - [ ] Create wireframes and mockups for the visual interface.
    - [ ] Develop dynamic visual elements to represent supply chain mappings and power dynamics.
    - [ ] **Optional Task**: Conduct user testing on wireframes to gather initial feedback.

2. **Implement Visualizations**:
    - [ ] Code the visual elements and integrate them into the system.
    - [ ] Ensure the visualizations are interactive and provide meaningful insights.

#### Sub-Goal 3: User Feedback Integration
1. **Collect Feedback**:
    - [ ] Conduct user testing sessions to gather feedback on the MVP and visual elements.
    - [ ] Use surveys and direct interviews to understand user needs and pain points.

2. **Integrate Feedback**:
    - [ ] Prioritize feedback and implement necessary changes to the system.
    - [ ] Continuously update the system based on ongoing user feedback.

#### Sub-Goal 4: System Testing and Quality Assurance
1. **Accuracy Testing**:
    - [ ] Develop test cases to evaluate the system's accuracy in supply chain mappings.
    - [ ] Implement an accuracy counter feature to provide users with confidence levels.

2. **Performance Testing**:
    - [ ] Conduct load testing to ensure the system performs well under various conditions.
    - [ ] Identify and resolve any performance bottlenecks.

3. **Quality Assurance**:
    - [ ] Perform comprehensive QA testing to identify and fix bugs.
    - [ ] Ensure the system meets all defined criteria for usability and accuracy.

#### Sub-Goal 5: Prepare for Visual Launch
1. **Documentation**:
    - [ ] Create detailed user documentation to guide users through the system.
    - [ ] Develop technical documentation for future development and maintenance.

2. **Marketing Materials**:
    - [ ] Prepare marketing materials to promote the visual launch.
    - [ ] Develop a demo video showcasing the system's capabilities.

3. **Launch Plan**:
    - [ ] Finalize the launch plan, including timelines and key milestones.
    - [ ] Coordinate with all stakeholders to ensure a smooth and successful launch.
