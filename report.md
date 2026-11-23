# Sentinel Awareness Project Report

**Project:** Sentinel Awareness — Social Engineering Awareness and Training Platform  
**Developer:** Edwin Msilimba  
**Programme:** BSc Computer Science  
**Institution:** DMI University

## Executive Summary

Sentinel Awareness is a web application for delivering authorised social engineering awareness exercises in a controlled environment. It combines fictional message simulations with consent management, immediate educational feedback, training modules, assessments, campaign analytics, and report exports.

The project is designed around a clear safety boundary: simulations are delivered through an internal application inbox, use fictional senders, and direct participants to educational content rather than credential collection. Participation is consent-based, and token handling and pseudonymous reporting help reduce unnecessary exposure of participant data.

## 1. Background and Problem

Social engineering exploits trust and decision-making, so awareness programmes need more than static information. Organisations also need a way to evaluate where participants may need additional support. Any practical exercise must be authorised, transparent, respectful of participant choice, and designed to avoid collecting real passwords or sensitive communications.

Sentinel Awareness addresses this need with a single system for campaign management, safe simulation, learning, assessment, and programme reporting. It provides administrators with structured tools and participants with a private environment for practice and feedback.

## 2. Aim and Objectives

The aim is to provide a safe and measurable platform for social engineering awareness and training.

The project objectives are to:

1. Let administrators create and manage campaigns and fictional scenarios.
2. Provide participants with a controlled inbox for authorised simulations.
3. Record delivery, opening, simulated-link, and reporting events.
4. Explain warning signs after a participant interacts with a simulation.
5. Provide training modules and pre- and post-training assessments.
6. Collect and manage informed consent, including withdrawal.
7. Support privacy-conscious, campaign-level and programme-level analytics.
8. Produce printable, PDF, and Excel reports for administrators.

## 3. Intended Users

### Administrators

Administrators manage participants, campaigns, scenarios, training content, and assessments. They can monitor campaign activity and learning outcomes, review consent status, and generate reports.

### Participants

Participants review consent information, use the simulation inbox, report suspicious messages, read educational guidance, complete training and assessments, and manage or withdraw their consent.

## 4. Main System Features

### Campaigns and scenarios

An administrator can create campaigns with objectives, date ranges, participant assignments, and one or more scenarios. Campaigns support draft, scheduled, active, paused, completed, and archived states. Scenarios contain fictional message details together with warning indicators and educational explanations.

### Simulation experience

The application delivers simulations to an internal participant inbox. The system records the campaign interaction lifecycle: assignment, delivery, opening, simulated-link interaction, reporting, and viewing the related learning guidance. Repeated events are deduplicated to avoid inflating campaign metrics.

### Training and assessment

Published training modules support self-paced learning. Administrators can create assessments with ordered questions, pass thresholds, and optional timing. Attempts capture scores, percentages, pass status, duration, and answer breakdowns, and support pre- and post-training comparisons.

### Analytics and reporting

Dashboards present campaign activity, participation and consent status, delivery/open/click/report rates, scenario performance, assessment outcomes, and training progress. Reports can be viewed for printing or exported to PDF and Excel for campaign-specific or institution-wide summaries.

## 5. Technical Design

The application uses Flask's application-factory pattern and groups routes into blueprints for authentication, administration, campaigns, participants, simulations, training, assessments, analytics, and reports. Service modules separate reusable business operations from HTTP route handling. SQLAlchemy models represent users, participants, consent, campaigns, scenarios, simulation events, training, assessments, and activity records.

```text
Participant or administrator browser
                 |
       Flask routes and blueprints
                 |
        Application service layer
                 |
        SQLAlchemy models and data
                 |
       MySQL/MariaDB deployment
       SQLite test configuration
```

Database changes are managed with Flask-Migrate and Alembic. The frontend uses HTML templates, CSS, JavaScript, Tailwind CSS, and Chart.js.

### Technology stack

| Area | Technologies |
| --- | --- |
| Language and web framework | Python 3.11–3.13, Flask 3 |
| Templates and interface | Jinja2, HTML, CSS, JavaScript, Tailwind CSS |
| Database and ORM | MySQL/MariaDB, SQLAlchemy; SQLite for tests |
| Migrations | Flask-Migrate, Alembic |
| Authentication and forms | Flask-Login, Flask-WTF, WTForms |
| Security and request controls | Werkzeug, Flask-Limiter |
| Charts and reporting | Chart.js, ReportLab, OpenPyXL, Pandas |
| Testing | Pytest, pytest-flask |

## 6. Consent, Privacy, and Safety

Consent is explicitly recorded and versioned. A participant may withdraw without giving a reason; withdrawal prevents future campaign assignments and revokes outstanding simulation tokens.

The application is intended for approved awareness programmes and has safeguards designed to keep exercises educational:

- Simulated messages use fictional senders and are delivered through the application inbox; external email is disabled by default.
- Simulated links lead to educational guidance, not real authentication forms.
- Simulation tokens are stored as SHA-256 digests, expire, and can be revoked.
- The system is designed not to collect real passwords, authentication codes, keystrokes, clipboard contents, or personal email messages.
- Role checks separate administrator and participant functions, and state-changing forms use CSRF protection.
- Password hashing, login-attempt controls, request rate limiting, secure response headers, and environment-based configuration provide additional protections.
- Participant-facing analytics and report exports use pseudonymous codes where appropriate.

These controls do not replace institutional policies or operational review. Campaigns should only be run with appropriate authorisation, participant consent, and oversight.

## 7. Typical Workflows

### Administrator workflow

1. Prepare fictional scenarios, training modules, and assessments.
2. Create a campaign, select its schedule, and assign eligible consenting participants.
3. Activate the campaign and monitor aggregate activity.
4. Review analytics, arrange follow-up learning, and generate reports.

### Participant workflow

1. Register and review the consent information.
2. Open the internal inbox and review simulated messages.
3. Report a message or follow its simulated link to see educational feedback.
4. Complete available training and assessments, or withdraw consent.

## 8. Testing and Evaluation

The repository includes a pytest-based test setup and test files. The application is structured so authentication and role-specific workflows can be exercised with a test configuration using SQLite.

The system provides measurable programme indicators, including simulation event rates, assessment outcomes, and training completion. Those indicators describe activity within a campaign; by themselves, they do not prove that a participant or organisation is protected from real attacks. No real-world effectiveness figures are claimed in this report. Such conclusions would require a separately designed evaluation with suitable consent, baseline measurements, and follow-up analysis.

## 9. Scope and Limitations

- Simulations are primarily delivered through the application's internal inbox; external email is disabled by default.
- Deployment requires environment-specific configuration, including a database and secure secret settings.
- Analytics reflect recorded application activity and should be interpreted as awareness-programme indicators, not as proof of fraud or security effectiveness.
- The quality of learning outcomes depends on suitable scenario content, responsible administration, and follow-up training.

## 10. Future Improvements

Possible future work includes expanded accessibility and mobile usability testing, richer learning content, approved institutional notification integrations, additional scheduling options, and more detailed organisational reporting. Any delivery integrations should preserve the project's consent and safety boundaries.

## Conclusion

Sentinel Awareness brings campaign administration, fictional simulations, consent controls, training, assessments, analytics, and reporting into one Flask application. Its focus on internal delivery, educational feedback, pseudonymous reporting, and withdrawal controls provides a foundation for responsible awareness exercises. Further evaluation and deployment-specific review are important before using the platform in a real institutional programme.

## Project Repository

[View the Sentinel Awareness source code on GitHub](https://github.com/portfoliodevme/social/tree/main/social_engineering_awareness).
