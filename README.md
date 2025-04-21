erDiagram
    %% Updated Entities with Oracle Data Types
    STUDENT {
        CHAR(4) student_id PK "NOT NULL"
        VARCHAR2(50) first_name
        VARCHAR2(50) last_name
        DATE date_of_birth
        VARCHAR2(50) email
        CHAR(10) phone
        VARCHAR2(50) address
        CHAR(4) dept_number FK
    }

    DEPARTMENT {
        CHAR(4) dept_number PK "NOT NULL"
        VARCHAR2(50) dname
        VARCHAR2(50) campus
        CHAR(4) mgr_ssn FK
        DATE mgr_start_date
    }

    COURSE {
        CHAR(9) course_code PK "NOT NULL"
        VARCHAR2(50) title
        NUMBER(2) credit_hours
        VARCHAR2(50) description
        CHAR(4) dept_number FK
    }

    LECTURER {
        CHAR(4) lecturer_id PK "NOT NULL"
        VARCHAR2(50) first_name
        CHAR(1) mi
        VARCHAR2(50) last_name
        DATE bdate
        VARCHAR2(50) address
        CHAR(1) sex
        NUMBER(10,2) salary
        CHAR(4) super_ssn FK
        CHAR(4) dept_number FK
    }

    ENROLLMENT {
        CHAR(6) enrollment_code PK "NOT NULL"
        CHAR(4) student_id FK
        CHAR(9) course_code FK
        DATE enrollment_date
        VARCHAR2(10) status
    }

    GRADE {
        CHAR(2) grade_code PK "NOT NULL"
        CHAR(6) enrollment_code FK
        NUMBER(5,2) assignment_score
        NUMBER(5,2) exam_score
        NUMBER(5,2) attendance_score
        NUMBER(5,2) final_grade
    }

    PAYMENT {
        CHAR(8) payment_code PK "NOT NULL"
        CHAR(4) student_id FK
        NUMBER(10,2) amount
        DATE payment_date
        VARCHAR2(20) method
        CHAR(20) transaction_id
    }

    %% Relationships with Cardinality Labels
    STUDENT ||--o{ ENROLLMENT : "enrolls in (1:N)"
    STUDENT ||--o{ PAYMENT : "makes (1:N)" 
    STUDENT }|--|| DEPARTMENT : "belongs to (N:1)" 

    LECTURER }|--|| DEPARTMENT : "assigned to (N:1)" 
    LECTURER ||--o{ COURSE : "teaches (1:N)" 

    COURSE ||--o{ ENROLLMENT : "has (1:N)" 
    COURSE }|--|| DEPARTMENT : "offered by (N:1)" 
    COURSE ||--o{ GRADE : "assessed through (1:N)" 

    ENROLLMENT }|--|| GRADE : "results in (1:1)" 

    %% Self-referencing relationship
    LECTURER ||--o{ LECTURER : "supervised by (1:N)"
