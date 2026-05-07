## Applied Math / Data Analysis Extensions

This project is also being used as an applied mathematics and data analysis platform.

Rather than treating the telemetry as simple dashboard data, the system will be used to study:

- rate of temperature and humidity change over time
- room-to-room temperature gradients
- rolling averages and smoothing
- variance and stability analysis
- threshold crossing frequency
- cumulative comfort/error metrics
- response lag after future vent adjustments
- vector/matrix representations of multi-room state
- feature engineering for anomaly detection and TinyML

This supports applied intuition for calculus, differential equations, linear algebra, statistics, and control systems while using real sensor data from the project itself.

Decision Support and Control Logic
This system is intended not only to collect and display telemetry, but also to support operational decisions.

Examples of system determinations include:

- normal environmental state
- threshold exceeded
- sustained alert condition
- degraded node communication
- invalid device input
- future actuator recommendations

Planned decision outputs include:
- system status classification
- severity level
- recommended human action
- future automated control actions
