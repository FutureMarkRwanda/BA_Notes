# **Learning Outcome 3: Monitor System Logs**

### 📘 Learning Hours: 20

---

## 📌 Objective

By the end of this section, learners will be able to:
- Configure logging strategies for different levels and formats.
- Design dashboards to visualize Key Performance Indicators (KPIs).
- Set up alerts and notifications based on technical requirements.

---

## 1. **Configuring Logging Strategies**

### 1.1 Definition
Setting up systems to capture, format, and store logs for monitoring.

### 1.2 Example: Log Configuration with ELK Stack
```bash
# Configure Logstash for log formatting
input { file { path => "/var/log/app.log" } }
output { elasticsearch { hosts => ["localhost:9200"] } }
```

### 1.3 Logging Aspects
| Aspect           | Description                              |
|------------------|------------------------------------------|
| Logging Levels   | Debug, Info, Error, etc.                |
| Log Aggregation  | Centralizing logs (e.g., ELK Stack)      |
| Security Logging | Tracking unauthorized access attempts    |

---

## 2. **Designing Dashboards**

### 2.1 Definition
Creating visual interfaces to display KPIs and log data for monitoring.

### 2.2 Example: Kibana Dashboard
```plaintext
1. Access Kibana at http://localhost:5601.
2. Create a dashboard.
3. Add visualization for CPU usage KPI.
```

---

## 3. **Configuring Alerts and Notifications**

### 3.1 Definition
Setting up automated alerts based on log events or thresholds.

### 3.2 Example: Alert in Prometheus
```yaml
groups:
- name: example
  rules:
  - alert: HighErrorRate
    expr: rate(http_errors[5m]) > 0.05
    for: 10m
    annotations:
      summary: "High error rate detected"
```

---

## ✅ Summary Table
| Concept               | Description                              | Example                        |
|-----------------------|------------------------------------------|--------------------------------|
| Logging Strategies    | Capturing and formatting logs            | ELK Stack configuration        |
| Dashboards            | Visualizing KPIs                         | Kibana CPU usage dashboard     |
| Alerts                | Automated notifications                   | Prometheus error rate alert    |

---

## 📚 Practice Exercises
1. Configure a logging strategy using Logstash to aggregate web server logs.
2. Design a dashboard in Grafana to monitor memory usage.
3. Set up an alert in Prometheus for high CPU usage (>80%).