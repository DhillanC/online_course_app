# Project Summary

Setup of base online course application

- Added initial project structure for the online course app.
- Includes Django app configuration, models, views, and templates for course management.
- ER diagram provided for upcoming assessment feature implementation.
- Default SQL database: SQLite3 (can be configured for PostgreSQL or MySQL based on deployment).
- Cloud deployment support (default: IBM Cloud Foundry).

## ER Diagram**


```mermaid

erDiagram
    auth_user {
        int id
        varchar password
        datetime last_login
        bool is_superuser
        varchar username
        varchar first_name
        varchar last_name
        varchar email
        bool is_staff
        bool is_active
        datetime date_joined
    }

    onlinecourse_course {
        int id
        varchar name
        varchar image
        varchar description
        datetime pub_date
        int total_enrollment
    }

    onlinecourse_lesson {
        int id
        int order
        text content
        int course_id
    }

    onlinecourse_question {
        int id
        text question_text
        int grade
        int lesson_id
    }

    onlinecourse_choice {
        int id
        text choice_text
        bool is_correct
        int question_id
    }

    onlinecourse_enrollment {
        int id
        date date_enrolled
        int mode
        int rating
        int course_id
        int user_id
    }

    onlinecourse_submission {
        int id
        int enrollment_id
    }

    onlinecourse_submission_choices {
        int id
        int submission_id
        int choice_id
    }

    onlinecourse_instructor {
        int id
        bool full_time
        int total_learners
        int user_id
    }

    onlinecourse_course_instructors {
        int id
        int course_id
        int instructor_id
    }

    onlinecourse_learner {
        int id
        varchar occupation
        varchar social_link
        int user_id
    }

    %% Relationships
    auth_user ||--o{ onlinecourse_enrollment : enrolls
    auth_user ||--o{ onlinecourse_learner : learns
    auth_user ||--o{ onlinecourse_instructor : instructs
    onlinecourse_course ||--o{ onlinecourse_lesson : contains
    onlinecourse_lesson ||--o{ onlinecourse_question : includes
    onlinecourse_question ||--o{ onlinecourse_choice : has
    onlinecourse_enrollment ||--o{ onlinecourse_submission : has
    onlinecourse_submission ||--o{ onlinecourse_submission_choices : includes
    onlinecourse_course ||--o{ onlinecourse_course_instructors : taught_by
    onlinecourse_instructor ||--o{ onlinecourse_course_instructors : teaches
