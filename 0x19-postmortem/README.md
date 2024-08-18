Postmortem: Database Connection Outage
Issue Summary

    Duration: The outage lasted from August 15, 2024, 14:00 UTC to August 15, 2024, 17:45 UTC.
    Impact: The primary service affected was the User Profile Management module. Users experienced errors when attempting to view or update their profiles. Approximately 75% of users were impacted.
    Root Cause: The root cause of the outage was a configuration error in the database connection pool settings, which led to a connection limit being exceeded.

Timeline

    14:00 UTC: The issue was detected when users began reporting errors and slow response times on the User Profile Management service.
    14:10 UTC: Monitoring tools alerted the engineering team to high response times and connection errors on the database.
    14:20 UTC: Initial investigation focused on the database server health and load balancing, with no anomalies found.
    14:45 UTC: Engineers noticed that the connection pool was exhausted, leading to a review of connection settings.
    15:00 UTC: It was discovered that the connection pool size had been incorrectly set to a very low number in the latest deployment.
    15:30 UTC: The configuration change was reverted, and connection pool settings were restored to the correct values.
    16:00 UTC: The service was gradually restored to normal operations, and monitoring confirmed that the issue was resolved.
    17:00 UTC: Final checks and validations were completed to ensure no further issues were present.
    17:45 UTC: Incident was formally resolved, and the root cause was documented.

Root Cause and Resolution

    Root Cause: The issue was caused by an incorrect database connection pool configuration in the application.properties file, which had been deployed as part of a recent update. The connection pool size was reduced to an insufficient number, which led to frequent connection timeouts and errors.
    Resolution: The connection pool configuration was corrected and redeployed. Specifically, the db.connection.pool.size setting was adjusted to the recommended value of 100, which resolved the connection timeout issues. Additionally, database connection monitoring was enhanced to detect such misconfigurations earlier.

Corrective and Preventative Measures

    Improvements/Fixes:
        Implement more stringent review and approval processes for configuration changes.
        Enhance automated testing to include validation of critical configuration settings.
        Improve monitoring and alerting for database connection pool metrics to detect misconfigurations early.

    Tasks to Address the Issue:
        Patch: Review and update the database connection pool configuration settings to recommended values.
        Monitor: Implement and configure alerts for connection pool usage and errors in the monitoring system.
        Review: Conduct a thorough review of recent configuration changes and deployment procedures to prevent similar issues.
        Document: Update the deployment checklist to include configuration validation steps.
        Test: Add automated tests to verify configuration settings as part of the deployment pipeline.

