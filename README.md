# Safety Monitoring on a Construction Site

## Project Overview
Our IEEE project focuses on making construction sites safer by detecting hazards at a construction site. This model watches out for unworn Personal Protective Equipment (PPE). It also addresses issues such as compromised safety nets, the proximity of people to Heavy Earth Moving Machinery (HEMM), and fire risks. 

Our specialty lies in our ability to:
- Spot damages to safety nets.
- Detect people near HEMMs.
- Identify flammable substances near fire sources—one of the most neglected hazards in a construction site.

When the model detects a problem, it sends alerts to on-site supervisors and workers so they can take immediate action. This timely intervention helps prevent accidents and ensures that everyone on site is better protected. By providing real-time updates, our model helps create a safer working environment.

---

## Hyper-Parameter Tuning and Model Training
After downloading and cloning the YOLOv5 requirements, we defined the number of classes in the `data.yaml` file. Due to memory and GPU constraints, an emphasis was placed on ensuring a working model. Thus, all hyper-parameters were fine-tuned accordingly.

- **Optimizer**: Stochastic Gradient Descent (SGD) with a default learning rate of `0.01` was used instead of the default YOLOv5 optimizer (Adam), as it would be computationally expensive.
- **Batch Size**: Maintained at the default value of `16`.
- **Image Size**: Kept at `640` pixels.
- **Epochs**: The model was trained for `90` epochs to ensure higher accuracy, adaptability to varied construction site conditions, and to avoid underfitting.

---

## Features
### Basic PPE (Personal Protective Equipment) Detection
- Ensures that workers are wearing PPE properly.
- Detects workers in elevators to ensure they are wearing safety harnesses.
- Identifies damaged safety nets, which are often neglected but crucial for preventing falls.

### Preventing Fire Accidents Caused by Sparks
- Ensures no inflammable objects are near welding or other spark-generating activities.
- Dataset includes sparks and three types of inflammable materials: cylinders, Styrofoam, and polythene.

#### Assumptions:
- Camera should be placed at eye level.
- Sparks can reach a distance of **7 meters (10.66 feet)**.

#### Implementation:
- A real-life distance of **7 meters** corresponds to **3338.079 pixels**.
- **Scale factor**: `7 / 3338.079 ≈ 0.002097`
- The **Euclidean distance** between sparks and inflammable objects is calculated. If this distance is ≤ **7 meters**, an alert is raised.

### Preventing Accidents Due to Heavy Earth Moving Machinery (HEMM)
- Many accidents occur because drivers cannot spot people in front of their vehicles.
- Dataset includes **people and all types of construction vehicles**.

#### Detection Steps:
1. **CSRT (Discriminative Correlation Filter with Channel and Spatial Reliability) Tracker** is used to track vehicles.
2. If a vehicle is moving, two safety checks are performed:
   - **Intersection Check**: If the bounding boxes of the vehicle and a person intersect, an immediate alert is raised.
   - **Proximity Check**: The **Euclidean distance** between the person and the vehicle is tracked across frames. If this distance reduces by half or more, an alert is raised.

---

## Results
- **PPE Detection Model**: **86% accuracy**.
- **Damaged Safety Nets & Harness Detection Model**: **93% accuracy** (as indicated by PR curves in Figure 3).
- **Fire Hazard Detection Model**: Works under specific conditions:
  - Camera placement at **eye level**.
  - Known distance between the **welding station and the camera**.
  - Sparks assumed to reach **up to 7 meters**.
- **HEMM Danger Zone Estimation Model**:
  - Could not be fully tested due to a lack of **high-quality video footage**.
  - Overall accuracy and real-world implementation **require further testing**.

---

## Scalability
The current models—PPE detection, safety net monitoring, and harness detection—show promising results. However, improvements are needed in **fire detection** and **HEMM safety**, which remain in early stages of testing. 

To scale the system, we propose:
- **Optimizing the model** for real-time performance.
- **Incorporating edge computing** for on-site deployment.
- **Using IoT-enabled devices** (e.g., smart helmets, sensors, and cameras) to monitor safety gear and proximity to machinery.
- **Cloud platforms** to manage data from multiple construction sites, enabling **predictive analytics** for better hazard detection and safety protocol refinement.

This scalable framework ensures **global deployment** while supporting real-time, localized hazard detection. Integrating **IoT with cloud-based systems** will also enable **predictive maintenance**, reducing equipment downtime and improving overall safety measures.

---

## Conclusion
Our model offers a **revolutionary approach** to monitoring safety in diverse construction environments. Unlike previous models that focused **only on object detection**, we go a step further by:

- **Establishing danger zones.**
- **Monitoring safe distances.**

This marks a significant improvement over traditional safety models, ensuring that **construction sites remain hazard-free and workers stay protected.**

---

## Contributors
- **Swastika Sharma**
- **Vedantika Sharma**
- **Arnav Satish**
- **Harshita Chhaparia**

