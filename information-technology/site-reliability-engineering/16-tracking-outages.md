## 16. Tracking outages
- Goal: track progress in improving reliability
- Functions:
  - Passively receive all alerts sent by the monitoring systems
  - Allow annotation, grouping & analyzing the data:
    - Aggregation: group multiple alerts together into a single incident
    - -> Also reduce speed of diagnosis
    - Tagging: provide info & allow general-purpose tagging to add metadata to notifications, at any level
    - -> Help with analysis
    - Analysis: functions by layers:
      - Bottom layer: counting & basic aggregate stats for reporting.
      Main stats eg: incidents per week/month/quarter & alerts per incident.
      - Next layer: comparison between teams/services and over time to identify first patterns and trends
      - Next layer: find wider issues requiring some semantic analysis
      (eg identifying the infra component causing most incidents
      -> potential benefit from increasing the stability/performance of this component)
  - Reporting & communication (ie send via email)