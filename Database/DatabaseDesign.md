# Database design

Database design is a critical aspect of creating efficient and scalable databases. 

### **Normalization**

**Normalization** is the process of organizing data in a database to reduce redundancy and improve data integrity. The main objectives of normalization are:

- Minimize duplicate data.
- Ensure data dependencies are properly enforced by using foreign keys.
- Simplify data management.

Normalization is achieved through a series of steps called **normal forms**, each with specific requirements.

### **Normal Forms**

1. **First Normal Form (1NF)**
   - **Definition**: A table is in 1NF if all its attributes contain only atomic (indivisible) values, and each value in a column must be of the same kind.
   - **Characteristics**:
     - No repeating groups or arrays.
     - Each column must contain unique values.
   - **Example**:
     - Non-1NF:  
       | EmployeeID | Name        | Skills           |
       |------------|-------------|-------------------|
       | 1          | John Doe   | SQL, C#, Python    |
       | 2          | Jane Smith | Java, JavaScript   |
     - Converted to 1NF:  
       | EmployeeID | Name        | Skill          |
       |------------|-------------|-----------------|
       | 1          | John Doe   | SQL             |
       | 1          | John Doe   | C#              |
       | 1          | John Doe   | Python          |
       | 2          | Jane Smith | Java            |
       | 2          | Jane Smith | JavaScript      |

2. **Second Normal Form (2NF)**
   - **Definition**: A table is in 2NF if it is in 1NF and all non-key attributes are fully functionally dependent on the primary key.
   - **Characteristics**:
     - Remove partial dependencies; non-key attributes must depend on the entire primary key.
   - **Example**:
     - Non-2NF:  
       | EmployeeID | Skill       | Department     |
       |-------------|-------------|-----------------|
       | 1          | SQL         | IT              |
       | 1          | C#          | IT              |
       | 2          | Java        | HR              |
     - Converted to 2NF:  
       **Employee Table**:  
       | EmployeeID | Department     |
       |-------------|-----------------|
       | 1          | IT              |
       | 2          | HR              |

       **Skills Table**:  
       | EmployeeID | Skill       |
       |-------------|-------------|
       | 1          | SQL         |
       | 1          | C#          |
       | 2          | Java        |

3. **Third Normal Form (3NF)**
   - **Definition**: A table is in 3NF if it is in 2NF and all the attributes are not only fully functionally dependent on the primary key but also are non-transitively dependent.
   - **Characteristics**:
     - Remove transitive dependencies; no non-key attribute should depend on another non-key attribute.
   - **Example**:
     - Non-3NF:  
       | EmployeeID | Department | Manager      |
       |-------------|------------|--------------|
       | 1          | IT         | Alice        |
       | 2          | HR         | Bob          |
     - Converted to 3NF:  
       **Department Table**:  
       | Department | Manager      |
       |-------------|--------------|
       | IT          | Alice        |
       | HR          | Bob          |

       **Employee Table**:  
       | EmployeeID | Department     |
       |-------------|-----------------|
       | 1          | IT              |
       | 2          | HR              |

4. **Boyce-Codd Normal Form (BCNF)**
   - **Definition**: A table is in BCNF if it is in 3NF and for every functional dependency (X → Y), X is a superkey.
   - **Characteristics**:
     - Ensures that there are no anomalies caused by functional dependencies.
   - **Example**:
     - Suppose you have:  
       | CourseID | Instructor  | Location     |
       |-----------|-------------|--------------|
       | CS101     | Dr. Smith   | Room 101     |
       | CS101     | Dr. Johnson | Room 102     |
       | CS102     | Dr. Smith   | Room 101     |
     - Here, the instructor determines the location but not the other way around. To convert to BCNF, you would split it into separate tables.

### **How to Structure Data to Reduce Redundancy**

- **Identify Entities**: Recognize the different entities (e.g., Employee, Department, Product).
- **Create Separate Tables**: For each entity, create a separate table.
- **Establish Relationships**: Use foreign keys to link related tables.
- **Eliminate Redundant Data**: Ensure that each piece of information is stored only once.

### **ER Modeling**

**Entity-Relationship (ER) Modeling** is a conceptual framework used to describe the data and its relationships in a database. Key components include:

- **Entities**: Objects or things in the database (e.g., Employee, Product).
- **Attributes**: Properties or characteristics of entities (e.g., Name, Price).
- **Relationships**: Associations between entities (e.g., an Employee sells a Product).
- **ER Diagrams**: Visual representations of entities, attributes, and relationships, helping to understand the database structure.

### **Data Modeling**

**Data Modeling** involves creating a conceptual representation of data structures and relationships. It consists of:

- **Conceptual Data Model**: High-level overview, focusing on what data is needed and its relationships without getting into the details.
- **Logical Data Model**: More detailed representation, specifying how data will be structured logically, including attributes and relationships.
- **Physical Data Model**: Details the actual implementation in a database management system (DBMS), including table structures, data types, and indexing strategies.