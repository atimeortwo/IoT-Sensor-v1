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

# Analysis Roadmap

## Purpose

This folder contains the applied math, data analysis, and future modeling work for the IoT sensor system.

The goal is to use real telemetry data to practice:
- calculus-based rate-of-change thinking
- statistical analysis
- system stability analysis
- control-oriented error metrics
- feature engineering for future TinyML/anomaly detection

## Current Data Available

- timestamp
- device_id
- temperature_f
- humidity
- threshold_f
- alert
- system_status
- recommended_action

## Phase 1: Descriptive Analysis

- mean temperature
- mean humidity
- max/min values
- alert counts
- time above threshold
- threshold crossing counts

## Phase 2: Rate and Trend Analysis

- temperature rate of change (dT/dt)
- humidity rate of change (dH/dt)
- rolling averages
- rolling variance
- trend direction over fixed windows

## Phase 3: Error and Control Metrics

- temperature error relative to threshold
- absolute error
- cumulative error over time
- duration of alert states
- future control error after vent actuation

## Phase 4: Multi-Node Analysis

- room-to-room temperature differences
- room-to-room humidity differences
- vector/state representation of multiple zones
- correlation between nodes
- identifying unstable or lagging zones

## Phase 5: Future Modeling / TinyML Prep

- feature engineering
- anomaly detection features
- stability metrics
- response lag analysis
- future control-system metrics
