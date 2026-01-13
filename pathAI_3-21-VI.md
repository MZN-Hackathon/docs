# Software Requirements Specification
# PathAI – AI-Powered Career Path Visualizer

**Version:** 3.2.IV  
**Prepared by:** Ibrahim Alselawi  
**Date:** 12.22.2025  

## Table of Contents
1. [Introduction](#1-introduction)
   1.1 [Purpose](#11-purpose)
   1.2 [Document Conventions](#12-document-conventions)
   1.3 [Project Scope](#13-project-scope)
   1.4 [References](#14-references)

2. [Overall Description](#2-overall-description)
   2.1 [Product Perspective](#21-product-perspective)
   2.2 [Product Features](#22-product-features)

3. [User Types and Permissions](#3-user-types-and-permissions)
   3.1 [User Classes Overview](#31-user-classes-overview)
   3.2 [User (Student)](#32-user-student)
   3.3 [Institution Representative](#33-institution-representative)
   3.4 [Company User](#34-company-user)
   3.5 [Admin](#35-admin)
   3.6 [Permission Matrix (Summary)](#36-permission-matrix-summary)
   3.7 [Assumptions](#37-assumptions)
   3.8 [Future Extensions](#38-future-extensions)

4. [System Features (Functional Requirements)](#4-system-features-functional-requirements)
   4.1 [AI Career Path Generation](#41-ai-career-path-generation)
   4.2 [Interactive Skill Tree Visualization](#42-interactive-skill-tree-visualization)
   4.3 [User Progress Tracking](#43-user-progress-tracking)
   4.4 [Learning Resource Recommendation Engine](#44-learning-resource-recommendation-engine)
   4.5 [Gamification System](#45-gamification-system)

5. [Nonfunctional Requirements (NFRs)](#5-nonfunctional-requirements-nfrs)
   5.1 [Performance Requirements](#51-performance-requirements)
   5.2 [Security Requirements](#52-security-requirements)
   5.3 [Reliability and Availability](#53-reliability-and-availability)
   5.4 [Maintainability](#54-maintainability)
   5.5 [Portability](#55-portability)

6. [Other Requirements](#6-other-requirements)

Appendix A: [Glossary](#appendix-a-glossary)  
Appendix B: [Future Enhancements](#appendix-b-future-enhancements)

---

## 1. Introduction

### 1.1 Purpose
This document specifies the software requirements for PathAI, an AI-powered web application designed to help students visualize and plan their career paths through an interactive skill tree system. The goal is to use artificial intelligence to map out the skills, knowledge areas, and learning resources necessary for users to reach their desired career objectives.

### 1.2 Document Conventions
- Functional requirements are denoted as FR-x.y.
- Non-functional requirements are denoted as NFR-x.y.
- "Shall" indicates a mandatory requirement; "Should" indicates a recommended but not mandatory one.

### 1.3 Project Scope
PathAI enables students to input a desired career goal (e.g., "Software Eng") and generates a personalized skill tree visualizing the skills and learning steps required to achieve it. The system also recommends educational resources and tracks the student's progress over time.

**Goals:**
- Provide AI-driven career guidance.
- Visualize learning paths in an interactive, game-like interface.
- Recommend learning resources dynamically.
- Track user progress and adapt the skill map over time.

### 1.4 References
- IEEE Std 830-1998, IEEE Recommended Practice for Software Requirements Specifications.
- O*NET Career Database (for standardized skill sets).
- OpenAI / Gemini API documentation (for AI integration)/ LLAMA.
- Firebase Documentation
- ADD MORE WHEN NEEDED

---

## 2. Overall Description

### 2.1 Product Perspective
PathAI is a standalone web application with client-side rendering and serverless backend integration via Firebase. It leverages external AI APIs to generate skill trees and learning paths dynamically.

### 2.2 Product Features
1. **AI Career Path Generator:** Converts a career goal into a structured skill map. This task is done by an admin user.
2. **Interactive Skill Tree Visualization:** Uses graph-based visualization to display skill relationships.
3. **Learning Resource Recommendation:** Suggests relevant online courses and projects.
4. **Progress Tracking:** Stores completed and in-progress skills per user.
5. **Gamification:** Awards badges or XP for learning milestones.
6. **Career Alternatives:** Suggests similar job roles based on learned skills.

---

## 3. User Types and Permissions

### 3.1 User Classes Overview
PathAI supports multiple user classes, each with defined permissions and system access levels. Role-based access control (RBAC) shall be enforced across all system features.

### 3.2 User (Student)
A User is an individual learner (student or self-learner) who uses PathAI to explore career paths, follow skill trees, and track personal learning progress.

**Permissions:**
- View published career paths and skill trees.
- Select a career goal from available paths.
- View skill details, prerequisites, and learning resources.
- Mark skills as:
  - Not started
  - In progress
  - Completed
- Track personal progress and earn badges/XP.
- Receive AI-suggested career alternatives based on progress.
- Update personal profile (name, preferences, skill level).
- Read-only access to career path structure.

**Restrictions:**
- Cannot create, edit, or publish career paths.
- Cannot modify skill dependencies or system data.
- Cannot access administrative or institutional dashboards.

### 3.3 Institution Representative
An Institution Representative represents an educational institution (e.g., university, college, training center). This role is responsible for aligning PathAI content with academic programs and institutional offerings.

**Permissions:**
- Create and manage an institution profile.
- Link institution programs, courses, or certifications to skills.
- Suggest learning resources related to institution offerings.
- View aggregated, anonymized student progress statistics for their institution.
- Submit career path suggestions or modifications for admin review.
- Manage institution-specific visibility (public/private programs).

**Restrictions:**
- Cannot directly publish or modify global career paths.
- Cannot access individual student private data.
- All submitted content requires admin approval.

### 3.4 Company User
A Company User represents an employer or organization that uses PathAI to promote job roles, internships, and skill requirements aligned with industry needs.

**Permissions:**
- Create and manage a company profile.
- Publish job listings, internships, or career advertisements.
- Define required skills for job roles (mapped to PathAI skill nodes).
- View aggregated talent insights (skills demand trends, not personal data).
- Suggest industry-relevant skill updates or emerging technologies.
- Promote sponsored career paths or skill tracks (subject to admin approval).

**Restrictions:**
- Cannot access individual user identities or progress.
- Cannot modify official skill trees directly.
- Advertisements and sponsored content require admin moderation.

### 3.5 Admin
Admin users are system operators and content curators responsible for maintaining PathAI's integrity, accuracy, and platform governance.

**Permissions:**
- Full access to all system features.
- Create, edit, validate, and publish career paths.
- Trigger AI career path generation.
- Edit AI-generated skill trees before publication.
- Approve or reject submissions from institutions and companies.
- Manage user roles and permissions.
- Monitor system logs, AI errors, and usage analytics.
- Manage gamification rules (badges, XP).
- Configure AI providers (OpenAI, Gemini, LLAMA).
- Manage Firestore data and system settings.

**Restrictions:**
- None (subject to internal governance policies).

### 3.6 Permission Matrix (Summary)

| Feature / Role | User | Institution Rep | Company User | Admin |
|----------------|------|----------------|--------------|-------|
| View Skill Trees | ✔ | ✔ | ✔ | ✔ |
| Track Progress | ✔ | ✖ | ✖ | ✔ |
| Generate Career Paths (AI) | ✖ | ✖ | ✖ | ✔ |
| Edit / Publish Skill Trees | ✖ | ✖ | ✖ | ✔ |
| Suggest Skills / Resources | ✖ | ✔ | ✔ | ✔ |
| Manage Ads / Job Listings | ✖ | ✖ | ✔ | ✔ |
| View Aggregated Analytics | ✖ | ✔ | ✔ | ✔ |
| Manage Users & Roles | ✖ | ✖ | ✖ | ✔ |

### 3.7 Assumptions
- All users authenticate via Firebase Authentication.
- Role information is stored securely in Firestore and enforced by security rules.
- Sensitive student data is never exposed to institutions or companies.
- All non-admin content submissions require moderation.

### 3.8 Future Extensions
- Mentor / Coach role (industry professionals).
- AI Validator role for automated content checking.
- Institution Admin (multi-representative support).

---

## 4. System Features (Functional Requirements)

### 4.1 AI Career Path Generation

#### 4.1.1 Description
The system shall generate a structured skill tree for a given career goal using AI. The skill tree will display categorized skills, dependencies, and recommended learning steps derived from AI processing (OpenAI, Gemini, LLAMA) and validated by O*NET standards.

#### 4.1.2 Rationale
Automating the creation of career-based skill trees allows consistent, data-driven career planning. It provides students with clear, AI-personalized pathways toward their professional goals.

#### 4.1.3 Inputs
- Career Goal Text: The name or description of the desired career (e.g., "Software Engineer").
- Optional Parameters: Skill level, domain focus, or learning duration (if provided by the user).

#### 4.1.4 Processing
1. The user enters a career title.
2. System sends the title to the AI API via HTTPS with context (e.g., related skills from O*NET).
3. AI processes the input and generates a JSON-based hierarchical structure of skills and dependencies.
4. System parses and formats this data into a skill tree model.
5. The generated skill tree is stored in Firestore.

#### 4.1.5 Outputs
Structured Skill Tree Object containing:
- Career name
- Skill categories
- Skill nodes (with prerequisites, descriptions, and recommended resources)
- Estimated learning duration per skill

#### 4.1.6 User Interface
- **Student Interface:** Read-only visualization of the published skill tree with skill details.

#### 4.1.7 Error Handling
- If AI API request fails, the system shall display a message: "The AI generation failed. Please check your network or try again later."
- If AI returns invalid data, the system shall log the error and fallback to predefined templates.
- Errors shall be recorded in Firestore logs with timestamp and user ID.

#### 4.1.8 Dependencies
- OpenAI / Gemini / LLAMA APIs (for AI generation).
- O*NET Database (for skill standardization).
- Firebase Firestore (for data storage).

#### 4.1.9 Constraints
- Requires active internet connection for AI API calls.
- AI output must comply with system data schema (careerPath document model).

#### 4.1.10 Verification
- Verify that generated trees contain valid skill nodes and hierarchical structure.
- Cross-check skill data against O*NET references.
- Test AI responses under different career titles and edge cases.
- Confirm that generated data is successfully stored in Firestore.

#### 4.1.11 Acceptance Criteria
- The system must generate a complete skill tree within 10 seconds for valid input.
- The skill tree must include at least one root skill and one dependency layer.
- Generated data must be editable by authorized users before publishing.
- Once published, students must be able to view the tree without errors.

### 4.2 Interactive Skill Tree Visualization

#### 4.2.1 Description
The system shall display AI-generated skill trees as interactive, graph-based visualizations. Users will be able to explore skill relationships, progress, and prerequisites in a dynamic and intuitive interface.

#### 4.2.2 Rationale
A visual skill tree allows users to better understand learning dependencies and progression. Interactive visualization enhances motivation, clarity, and user engagement, making career planning easier to comprehend.

#### 4.2.3 Inputs
- Skill Tree Data Object retrieved from Firestore (generated by AI).
- User Progress Data (completed/in-progress skills).
- Device Display Information (screen size, orientation).

#### 4.2.4 Processing
1. System loads skill tree data for the selected career path.
2. Visualization library (e.g., D3.js or Cytoscape.js) renders nodes and edges dynamically.
3. User interactions (click, hover, zoom) are captured and used to highlight or expand nodes.
4. System overlays progress data to color-code skill nodes based on completion state.
5. User interface updates in real time when progress changes are detected via Firestore listeners.

#### 4.2.5 Outputs
- Rendered Skill Tree Visualization (SVG or Canvas).
- Dynamic Node Information Panel displaying skill details, related resources, and progress.
- Real-time Updated View reflecting user progress or admin modifications.

#### 4.2.6 User Interface
**Visual Elements:**
- Skill nodes (circular or rectangular).
- Edges connecting prerequisite relationships.
- Color coding (e.g., gray = locked, yellow = in progress, green = completed).

**Controls:**
- Zoom in/out, drag to pan.
- Click to expand/collapse branches.
- Hover to preview skill details.

**Responsiveness:**
- Auto-layout adapts to mobile, tablet, and desktop screens.
- The tree maintains center alignment regardless of device.

#### 4.2.7 Error Handling
- If tree data is missing or corrupted, display: "Skill tree not available. Please regenerate or contact your administrator."
- If visualization rendering fails, fall back to a list-based layout.
- Log rendering or data errors to Firestore with user ID and timestamp.

#### 4.2.8 Dependencies
- D3.js or Cytoscape.js visualization library.
- Firebase Firestore (for data and progress).
- Framework7 (for page and layout rendering) WILL CHOOSE LATER.

#### 4.2.9 Constraints
- Visualization performance depends on device GPU/CPU capabilities.
- Skill trees larger than 300 nodes may require progressive rendering or pagination.
- Internet connection is required for data synchronization.

#### 4.2.10 Verification
- Verify skill nodes and dependencies render correctly for various data sizes.
- Test interactions (click, zoom, drag) on multiple browsers and devices.
- Confirm real-time updates occur when progress changes.
- Validate color codes correspond correctly to user progress states.

#### 4.2.11 Acceptance Criteria
- The skill tree shall render completely within 3 seconds for an average-size tree (<100 nodes).
- The user shall be able to click and expand nodes without lag.
- The tree must correctly display completion states (color-coded).
- The interface must remain responsive and functional on desktop and mobile devices.

### 4.3 User Progress Tracking

#### 4.3.1 Description
The system shall allow users to track their learning progress across AI-generated skill trees. Users shall be able to mark individual skills as not started, in progress, or completed. The system shall persist progress data, calculate milestones, and update the skill tree visualization in real time.

#### 4.3.2 Rationale
Tracking progress provides learners with motivation, structure, and measurable advancement toward career goals. It enables adaptive learning paths, gamification features, and personalized career recommendations while offering insights into skill acquisition over time.

#### 4.3.3 Inputs
- Skill Identifier (Skill ID).
- User Identifier (User ID).
- Progress Status:
  - Not Started
  - In Progress
  - Completed
- Optional User Notes or Reflections.
- Timestamp of Progress Update.

#### 4.3.4 Processing
1. User selects a skill node within the skill tree.
2. User updates the progress status of the skill.
3. System validates that the skill belongs to the selected career path.
4. System updates the user's progress record in Firestore.
5. System recalculates:
   - Completion percentage of the career path.
   - XP and badge eligibility (if applicable).
6. Firestore real-time listeners notify the client.
7. Skill tree visualization updates node colors and progress indicators.
8. Dependent skills may be unlocked if prerequisites are completed.

#### 4.3.5 Outputs
- Updated User Progress Record stored in Firestore.
- Visual update of skill node state (color-coded).
- Updated career completion percentage.
- XP, badge, or milestone notifications (if triggered).

#### 4.3.6 User Interface
**Student Interface:**
- Clickable skill nodes with progress toggle.
- Visual indicators:
  - Gray: Not Started
  - Yellow: In Progress
  - Green: Completed
- Progress dashboard showing:
  - Overall completion percentage.
  - Completed vs remaining skills.
  - Recent activity timeline.

**Admin Interface:**
- Read-only aggregated progress analytics.
- No access to individual student notes or private data.

#### 4.3.7 Error Handling
- If progress update fails, the system shall display: "Unable to save progress. Please check your connection and try again."
- If invalid Skill ID or Career Path mismatch is detected:
  - The system shall reject the update.
  - An error log shall be recorded with timestamp and User ID.
- Conflicting updates shall be resolved using last-write-wins strategy.

#### 4.3.8 Dependencies
- Firebase Authentication (user identity).
- Firebase Firestore (progress storage and real-time updates).
- Skill Tree Data Model.
- Visualization module (Section 4.2).

#### 4.3.9 Constraints
- Internet connection is required for real-time synchronization.
- Offline progress updates may be queued and synchronized when connectivity is restored.
- Progress data is scoped per user and per career path.

#### 4.3.10 Verification
- Verify that progress updates persist correctly in Firestore.
- Verify real-time UI updates upon progress changes.
- Confirm prerequisite-based unlocking logic functions correctly.
- Test progress tracking across multiple devices for the same user.
- Validate that unauthorized users cannot modify other users' progress.

#### 4.3.11 Acceptance Criteria
- Users shall be able to update skill progress within 1 second.
- Progress changes shall reflect visually without page reload.
- Completion percentage shall update accurately.
- Completed prerequisite skills shall unlock dependent skills.
- User progress data shall persist across sessions and devices.

### 4.4 Learning Resource Recommendation Engine

#### 4.4.1 Description
The system shall provide personalized learning resource recommendations to users based on their selected career path, completed skills, and current progress. Resources include online courses, tutorials, projects, certifications, and articles. Recommendations shall be dynamically generated using AI APIs (OpenAI, Gemini, LLAMA) and curated databases (e.g., O*NET, institution/course catalogs).

#### 4.4.2 Rationale
Providing targeted learning resources ensures that students can effectively acquire the skills necessary for their career goals. AI-driven recommendations increase relevance and reduce cognitive overload by prioritizing resources aligned with user progress and skill gaps.

#### 4.4.3 Input
- User Identifier (User ID)
- Selected Career Path / Skill Tree
- Completed/In-progress Skills (from Section 4.3)
- Optional Parameters:
  - Preferred learning style (video, text, hands-on)
  - Target learning duration
  - Institution or company preference (optional)

#### 4.4.4 Processing
1. System retrieves the user's current skill progress.
2. For each skill node not yet completed:
   - Query AI API for recommended resources.
   - Retrieve resources linked to institutions or companies (if applicable).
3. Filter and rank resources based on:
   - Skill relevance
   - Learning duration
   - User preferences
   - Resource availability and credibility
4. Format resources into a structured object with:
   - Resource name
   - Type (course, project, article, certification)
   - Provider / source
   - URL / access link
   - Estimated learning duration
   - Prerequisites or required skills
5. Store recommendations in Firestore for real-time user access.
6. Update recommendations dynamically as the user completes skills or changes preferences.

#### 4.4.5 Outputs
- Structured Resource Recommendation Object containing:
  - Skill ID(s) linked to each resource
  - Resource metadata (name, type, provider, link, duration)
  - Priority / ranking score
- Real-time updated recommendation panel in the user interface.

#### 4.4.6 User Interface
**Student Interface:**
- Resource cards displayed per skill or skill category.
- Filters and sorting:
  - Type (video, text, project, certification)
  - Duration
  - Popularity / rating (if available)
- Clickable links to access resources directly.

**Admin Interface:**
- View aggregated recommendations.
- Add, approve, or remove curated resources.
- Adjust AI recommendation parameters (priority weights, sources).

#### 4.4.7 Error Handling
- If AI API fails or times out: "Resource recommendations are temporarily unavailable. Please try again later."
- If no relevant resources are found: Display fallback curated resources.
- Log all API errors with timestamp and User ID in Firestore for debugging.

#### 4.4.8 Dependencies
- AI APIs (OpenAI, Gemini, LLAMA)
- O*NET or other skill-resource databases
- Firestore (recommendation storage and real-time updates)
- Skill Tree Module (Section 4.2)
- User Progress Module (Section 4.3)

#### 4.4.9 Constraints
- Internet connection required for AI-generated recommendations.
- Recommendation generation must complete within 5 seconds per user query.
- AI output must comply with the system data schema for Resource Recommendation Objects.

#### 4.4.10 Verification
- Verify recommendations match user's skill gaps and career path.
- Test AI API response parsing and mapping to resource objects.
- Validate filtering and sorting functionality.
- Confirm real-time updates are correctly reflected in the UI.
- Ensure fallback resources display when AI fails or returns empty results.

#### 4.4.11 Acceptance Criteria
- Users shall receive at least 3 recommended resources per uncompleted skill.
- Resource panel shall update dynamically as progress changes.
- AI-generated recommendations shall be relevant to skill nodes in at least 90% of test cases.
- Curated fallback resources shall display if AI recommendation fails.
- Students shall be able to access resource links directly without errors.

#### 4.4.12 Future Extensions
- Personalized recommendations based on learning behavior and past engagement.
- Integration with institutions or company-specific courses and certifications.
- AI-driven prioritization of learning paths based on skill difficulty and user progress.
- Rating and feedback system for recommended resources.

### 4.5 Gamification System

#### 4.5.1 Description
The system shall provide a gamification layer that motivates and engages users by rewarding progress through the skill tree. Users earn Experience Points (XP), badges, and milestones based on completing skills, using recommended resources, and achieving learning milestones. Gamification integrates with progress tracking (4.3) and resource recommendations (4.4) to enhance learning engagement and retention.

#### 4.5.2 Rationale
Gamification increases motivation, engagement, and goal completion. By linking rewards to skill completion and resource utilization, PathAI encourages consistent learning, fosters a sense of achievement, and provides measurable feedback on career progress.

#### 4.5.3 Inputs
- User Identifier (User ID)
- Skill Completion Status (from 4.3)
- Resource Usage (from 4.4)
- Career Path ID / Skill Tree ID
- Optional:
  - Daily streaks
  - Challenge completions

#### 4.5.4 Processing
1. System monitors skill completion and resource usage in real-time.
2. Assigns XP for each action:
   - Completing a skill node → base XP
   - Completing a recommended resource → additional XP
   - Completing all skills in a category → bonus XP
3. Evaluate milestones for badge assignment:
   - "First Skill Completed"
   - "Skill Category Mastery"
   - "Resource Completion Streak"
4. Update user profile with new XP and badges.
5. Trigger real-time UI updates to reflect changes.
6. Aggregate leaderboard data (optional, anonymous) for friendly competition.

#### 4.5.5 Outputs
- Updated XP value per user
- Awarded badges/milestones
- Visual feedback in UI:
  - Skill node progress colors (linked to XP)
  - Badge notifications and achievement popups
  - Progress bars for career completion
- Optional leaderboard rankings

#### 4.5.6 User Interface
**Student Interface:**
- Skill nodes display progress and XP rewards.
- Badge notifications pop up when milestones are achieved.
- Career dashboard shows total XP, earned badges, and skill completion stats.
- Optional leaderboard shows rank among peers (anonymous).

**Admin Interface:**
- Configure XP rules (per skill, per resource).
- Define badges, milestones, and achievement criteria.
- Monitor leaderboard metrics and gamification analytics.

#### 4.5.7 Error Handling
- If XP or badge updates fail: "Unable to update gamification data. Progress is still saved."
- Log errors in Firestore with User ID and timestamp.
- Prevent duplicate badge assignments.
- Validate XP calculations to avoid inconsistencies.

#### 4.5.8 Dependencies
- Progress Tracking Module (4.3) for skill completion data
- Resource Recommendation Module (4.4) for bonus XP
- Firestore for storing XP, badges, and milestone data
- Skill Tree Visualization Module (4.2) for dynamic updates
- Optional: Leaderboard aggregation module

#### 4.5.9 Constraints
- Real-time updates require an active internet connection.
- XP and badge calculations must be consistent across devices.
- Gamification layer shall not allow students to artificially inflate XP (anti-cheat rules applied).
- Badges and milestones are role-specific (admin-only configuration).

#### 4.5.10 Verification
- Verify XP increments correctly for each skill or resource completed.
- Confirm badges/milestones trigger accurately based on rules.
- Test UI updates in real-time on multiple devices.
- Ensure leaderboard reflects only valid, anonymized data.
- Validate admin configuration changes apply correctly to all users.

#### 4.5.11 Acceptance Criteria
- Users shall earn XP and badges immediately upon skill or resource completion.
- Skill tree nodes shall reflect gamification states (color-coded, XP icons).
- Users shall see a milestone notification when a badge is achieved.
- Gamification data shall persist across sessions and devices.
- Admins shall be able to configure rules without downtime.

#### 4.5.12 Future Extensions
- Challenges and quests: multi-skill or cross-skill objectives.
- Seasonal or time-limited achievements.
- Peer comparison and mentor feedback integration.
- AI-driven personalized reward suggestions.

---

## 5. Nonfunctional Requirements (NFRs)

These cover quality attributes and constraints, including performance, security, maintainability, availability, and portability.

### 5.1 Performance Requirements
- Maximum acceptable response time for skill tree generation (e.g., <10 seconds).
- Resource recommendation response time (e.g., <5 seconds).
- Real-time updates for progress tracking and gamification (e.g., <1 second).

### 5.2 Security Requirements
- Firebase Authentication for all users.
- Role-based access control (RBAC) enforced by Firestore rules.
- Sensitive user data (progress, profile) encrypted at rest and in transit (future).
- Admin-only permissions for AI generation, publishing, and moderation.

### 5.3 Reliability and Availability
- System uptime ≥ 99.9999% (firebase).
- AI API fallback or cached templates in case of downtime.
- Offline-first support for progress tracking (sync when online firebase).

### 5.4 Maintainability
- Modular architecture: separate modules for AI generation, visualization, progress, recommendations, and gamification.
- Clear documentation for adding new career paths, skills, or resource sources.

### 5.5 Portability
- Web application compatible with major browsers (Chrome, Firefox, Edge, Safari).
- Responsive design for desktop, tablet, and mobile.
- Optional PWA (Progressive Web App) support.

---

## 6. Other Requirements
*To be defined as needed during development.*

---

## Appendix A: Glossary

**AI Career Path Generator:** System component that uses artificial intelligence to create structured skill trees from career goal inputs.

**Firebase:** Google's mobile and web application development platform used for backend services.

**Firestore:** Firebase's NoSQL cloud database used for storing application data.

**O*NET:** Occupational Information Network, a comprehensive database of occupational requirements and worker attributes.

**PWA:** Progressive Web App, a type of application software delivered through the web.

**RBAC:** Role-Based Access Control, a method of regulating access to computer or network resources based on roles.

**Skill Tree:** A hierarchical visualization of skills and their dependencies required for a specific career path.

**XP:** Experience Points, a gamification metric representing user progress and achievements.

---

## Appendix B: Future Enhancements

1. **Advanced Analytics Dashboard:** Detailed insights into learning patterns, skill acquisition rates, and career progression trends.

2. **Social Learning Features:** Peer networking, study groups, and mentor matching capabilities.

3. **Integration with Learning Platforms:** Direct integration with platforms like Coursera, Udemy, edX, and LinkedIn Learning.

4. **Job Market Integration:** Real-time job market data and salary information for different career paths.

5. **AI Career Coach:** Advanced AI assistant providing personalized career advice and learning guidance.

6. **Multi-language Support:** Internationalization for global user base.

7. **Advanced Reporting:** Customizable reports for institutions and companies.

8. **API for Third-party Integration:** Allow other educational platforms to integrate with PathAI's skill tree system.

9. **Mobile Applications:** Native iOS and Android applications.

10. **Virtual Reality Visualization:** Immersive VR experience for exploring career paths.