# Phase 0 Project Charter: Pilot AI Drill - ROP Prediction

## 1.0 Project Identification

- **Project Title**: Pilot AI Drill - Intelligent Rate of Penetration (ROP) Prediction
- **Phase**: 0 - Problem Definition and Feasibility Assessment
- **Domain**: Drilling Optimization for Geothermal/Energy Wells
- **Data Source**: Utah FORGE Well 16-16B(78)-32 Mud Logging Data (LAS Format)

## 2.0 Business Context and Problem Statement

### 2.1 Business Problem

The drilling process represents a significant portion of well construction costs and timelines. Inefficient drilling rates directly impact project economics through extended rig time, increased operational costs, and delayed revenue generation. Current methods for predicting and optimizing Rate of Penetration (ROP) face significant limitations in accuracy and adaptability to complex downhole conditions.

### 2.2 Technical Problem

Traditional mechanistic ROP models struggle with complex, variable downhole environments, resulting in prediction difficulties and low accuracy . While data-driven machine learning models have shown promise, they often lack mechanistic constraints, limiting their performance to specific conditions and reducing real-world applicability . The fundamental challenge lies in developing a predictive model that balances physical understanding with data-driven insights while maintaining generalizability across different drilling conditions.

## 3.0 Technical Background

### 3.1 Rate of Penetration (ROP) Significance

ROP serves as a crucial Key Performance Indicator (KPI) for drilling efficiency, directly influencing operational costs and project timelines. Accurate ROP prediction enables:

- Optimization of drilling parameters in real-time
- Reduction of non-productive time (NPT)
- Enhanced bit life and tool utilization
- Improved wellbore quality and placement

### 3.2 Domain Fundamentals

The drilling process involves complex interactions between surface controls and subsurface conditions. Primary factors influencing ROP include :

- **Mechanical Parameters**: Weight on Bit (WOB), rotary speed (RPM), torque
- **Formation Characteristics**: Rock type, hardness, mineral composition
- **Hydraulic Factors**: Mud properties, flow rates, equivalent circulating density
- **Environmental Conditions**: Depth, temperature, pressure

## 4.0 Data Foundation Assessment

### 4.1 Available Data Structure

Based on the provided LAS file sample, the dataset encompasses:

**Depth Data**: 90.0 to 10,947.5 feet with 1.0 ft sampling interval
**Null Values**: -999.25 standard null indicator

### 4.2 Key Data Categories Available

| **Category** | **Parameters** | **Units** | **Data Quality Notes** |
|--------------|----------------|-----------|------------------------|
| **Depth Reference** | DMEA | ft | Primary depth index |
| **Drilling Mechanics** | WOBI (Weight on Bit), TQI (Torque), RPMI (RPM) | Klb, FtLb, - | Critical direct parameters |
| **Target Variable** | ROPA | ft/hr | Rate of Penetration - measurement interval |
| **Formation Mineralogy** | ANH, CAL, CHL, EPI, HEM, PYR, QTZ, SER, SIL | - | Lithological composition indicators |
| **Environmental** | MTIA (Mud Temp In), MTOA (Mud Temp Out) | F | Temperature measurements |
| **Gas Measurements** | AH2S1, AH2S2, AH2S3, AH2S4 | ppm | H2S at different locations |

### 4.3 Initial Data Quality Observations

Preliminary assessment indicates significant data quality challenges that will require attention in subsequent phases:

- Extensive null values (-999.25) across multiple parameters
- Potential sensor measurement gaps or operational artifacts
- Variable data density across different depth intervals
- Need for comprehensive lag time calculation for depth correlation

## 5.0 Project Objectives and Success Criteria

### 5.1 Phase 0 Objectives

1. Define precise problem scope and measurable success criteria
2. Assess data adequacy and identify critical gaps
3. Establish technical feasibility of ML approaches
4. Develop detailed project roadmap for subsequent phases
5. Identify key stakeholders and resource requirements

### 5.2 Success Criteria for Subsequent Phases

| **Metric Category** | **Target** | **Measurement Method** |
|---------------------|------------|------------------------|
| **Prediction Accuracy** | MAE < 10 ft/hr | Mean Absolute Error on test set |
| **Model Performance** | R² > 0.75 | Coefficient of determination |
| **Error Tolerance** | RMSE < 15 ft/hr | Root Mean Square Error |
| **Business Impact** | 15-25% ROP improvement | Comparative analysis with historical performance |

## 6.0 Technical Approach Considerations

### 6.1 Proposed Methodology

Based on current research, a hybrid approach combining mechanistic understanding with machine learning shows significant promise . This methodology leverages:

- **Physical Model Foundation**: Incorporation of established drilling physics
- **Machine Learning Enhancement**: Data-driven pattern recognition for non-linear relationships
- **Transfer Learning Capabilities**: Knowledge application across different well conditions

### 6.2 Anticipated Technical Challenges

1. **Data Quality**: Significant missing values and potential measurement artifacts
2. **Multi-scale Relationships**: Complex interactions between drilling parameters and formation properties
3. **Temporal Dynamics**: Time-dependent effects and lag relationships in drilling data
4. **Physical Consistency**: Ensuring model predictions align with fundamental drilling mechanics

## 7.0 Phase 0 Deliverables

1. **Problem Definition Document** (This charter)
2. **Data Quality Assessment Report**
3. **Stakeholder Alignment and Sign-off**
4. **Detailed Project Plan for Phases 1-5**
5. **Resource and Infrastructure Requirements**
6. **Risk Assessment and Mitigation Strategies**

## 8.0 Path Forward

Upon approval of this Phase 0 charter, the project will proceed to Phase 1 (EDA and Data Preprocessing) with the following immediate next steps:

1. **Data Acquisition**: Complete download and validation of full dataset from <https://gdr.openei.org/submissions/1516>
2. **Environment Setup**: Establish computational infrastructure and version control
3. **Stakeholder Review**: Formal review and sign-off on problem definition
4. **Team Mobilization**: Assign core team members and define responsibilities

---
