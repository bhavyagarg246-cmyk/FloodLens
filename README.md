FLOODLENS
AI-ASSISTED ROAD HAZARD REPORTING AND GEOGRAPHICAL HOTSPOT IDENTIFICATION

1. OVERVIEW

FloodLens is a road-hazard reporting and analysis platform designed to make road problems easier to identify, document, and prioritize. It combines AI-assisted pothole detection from uploaded images with structured, location-based reporting and geographical hotspot identification.

Road hazards can create safety risks, disrupt travel, and increase maintenance costs. However, information about these issues is often scattered across individual complaints, photographs, and local observations. FloodLens aims to bring this information into an organized workflow so that recurring problem areas become easier to recognize.

Although the project name refers to floods, the currently integrated computer-vision model focuses on pothole detection. Waterlogging or floodwater detection and flood-risk prediction are potential future extensions, not capabilities that should be assumed to be implemented in the current version.

2. PROBLEM STATEMENT

Road users regularly encounter potholes, damaged road surfaces, and other hazards that may be difficult to report consistently. Reports can be scattered across different channels, lack standardized details, or provide insufficient location information. As a result, it can be challenging to understand where hazards occur repeatedly and which areas may deserve closer inspection.

Manual identification and verification can require considerable time and effort. Image-only detection systems can identify visible objects but may not connect detections to recurring problems across different locations. Similarly, unstructured complaints may not provide a clear geographical picture.

There is a need for a practical workflow that combines image-based assistance, structured hazard reports, and geographical grouping to improve the visibility of road issues and support informed inspection priorities.

3. PROPOSED SOLUTION

FloodLens provides a unified workflow for AI-assisted pothole detection and location-aware hazard reporting. Users can upload a road image for analysis and submit reports containing information such as location, description, severity, and geographical coordinates when available.

The application processes uploaded images through a computer-vision pipeline and returns detection results. Reports can be stored and retrieved through the backend, while geographical hotspot logic groups nearby reports to highlight areas where hazards have been reported repeatedly.

The purpose is not to replace on-site inspection or official decision-making. Instead, FloodLens is designed to organize evidence and make reported hazards easier to review and prioritize.

4. KEY FEATURES

A. AI-ASSISTED POTHOLE DETECTION

- Accepts supported road-image uploads, including JPG, JPEG, PNG, and WEBP.
- Uses a YOLOv8 model through the Ultralytics framework to detect potholes.
- Returns detection information such as bounding boxes, detection count, confidence scores, and an annotated image.
- Uses a configured confidence threshold of 0.35 to filter predictions below that threshold.

A confidence score reflects how confident the model is in a particular prediction. It is not the same as overall model accuracy or a guarantee that a detection is correct.

B. STRUCTURED HAZARD REPORTING

- Supports recording reports with details such as location name, description, and severity.
- Supports latitude and longitude when available.
- Organizes hazard information in a consistent format rather than leaving it as an isolated complaint.

C. GEOGRAPHICAL HOTSPOT IDENTIFICATION

- Uses geographical coordinates to group nearby reports.
- The current logic considers reports within an approximate 500-metre radius.
- Three or more reports can qualify an area as a hotspot.
- Five or more reports can qualify as a high-level hotspot under the current rules.
- Hotspot identification indicates a concentration of reports, not proof of flooding or a prediction of future danger.

D. REPORT STATUS TRACKING

Reports can have statuses such as Unverified, Corroborated, and Resolved. These statuses help organize the reporting lifecycle, but they should not be interpreted as independent proof that every report has been physically verified.

E. IMAGE ANALYSIS API

The Flask backend provides an image-analysis endpoint that accepts an uploaded image, invokes the analysis pipeline, and returns structured results along with a URL for the processed image.

5. SYSTEM WORKFLOW

STEP 1: IMAGE UPLOAD OR REPORT SUBMISSION

A user uploads a supported road image for analysis and/or submits a hazard report with relevant details.

STEP 2: BACKEND HANDLING

The Python Flask backend validates and handles the image upload and coordinates the analysis process.

STEP 3: AI INFERENCE

The YOLOv8-based detection module analyzes the image and produces pothole predictions, bounding boxes, confidence scores, a detection count, and an annotated image.

STEP 4: RESULT GENERATION

The analysis pipeline organizes the detection output and produces a structured response for the frontend.

STEP 5: REPORT STORAGE

Report details are managed through the application's database layer, which uses PostgreSQL for report data.

STEP 6: GEOGRAPHICAL GROUPING

When reports contain usable latitude and longitude, the hotspot logic evaluates their geographical proximity and identifies clusters according to the configured rules.

STEP 7: REVIEW AND PRIORITIZATION

The resulting detection information and clusters can help users or relevant teams understand where reported hazards are concentrated and decide which locations may need further inspection.

6. TECHNOLOGY STACK

- Programming Language: Python
- Backend Framework: Flask
- Computer Vision: YOLOv8 through Ultralytics
- Database: PostgreSQL
- Frontend: HTML, CSS, and JavaScript
- Image Processing: Image upload, model inference, and annotated-image output
- Geospatial Logic: Latitude/longitude-based distance calculation and report clustering
- Deployment: AWS has been identified as part of the project setup; the exact deployment configuration should be documented separately if required.

7. HOW FLOODLENS DIFFERS FROM TRADITIONAL APPROACHES

Traditional road-hazard reporting may depend on manual inspection and complaints spread across different channels. FloodLens brings image analysis, structured reports, and geographical hotspot identification into a single workflow.

Its key distinctions are:

- AI-assisted identification of potholes in images.
- Structured recording of hazard details.
- Geographical grouping of nearby reports.
- Report-status organization.

An image-only detector may identify a pothole in one photograph but not reveal whether similar issues have been reported nearby. A reporting-only system may collect complaints without providing AI-assisted visual analysis. FloodLens aims to connect these capabilities so that individual reports can contribute to a broader view of recurring problem areas.

This is a design advantage, not a claim that FloodLens has already outperformed every existing product. Any claim of higher accuracy, lower cost, or faster response should be supported by measured comparisons and field testing.

8. EXPECTED IMPACT

FloodLens is intended to:

- Make road hazards easier to document.
- Reduce dependence on purely manual visual identification during initial screening.
- Organize reports in a consistent format.
- Reveal geographical concentrations of reported hazards.
- Help guide inspection and maintenance priorities.
- Create a foundation for broader, data-informed road-safety workflows.

The platform supports decision-making rather than replacing official verification, engineering assessment, or emergency services.

9. FEASIBILITY AND LIMITATIONS

The project uses established technologies: Flask for backend APIs, YOLOv8 for computer vision, PostgreSQL for structured report data, and standard web technologies for the user interface. This modular structure makes the current workflow practical to develop and provides a path for incremental improvement.

The quality of results depends on image quality, model performance, reliable location data, and the completeness of user reports. A confidence threshold does not establish model accuracy. Hotspot rules identify clusters of reports and do not establish the physical severity of a hazard. Reports may also be duplicated, inaccurate, or not yet verified.

The currently integrated model focuses on potholes. Floodwater or waterlogging detection, flood-depth estimation, flood forecasting, and safe-route recommendations should not be presented as existing features unless they have been implemented and tested.

10. FUTURE SCOPE

Potential future extensions include:

- Training and validating a dedicated waterlogging or floodwater detection model.
- Combining reports with rainfall, river-level, weather, and official flood information.
- Adding duplicate-report detection and stronger verification workflows.
- Evaluating model performance using a labelled test dataset.
- Developing time-aware hotspot trends and severity-based prioritization.
- Adding map-based visualization and operational dashboards.
- Exploring safer-route recommendations after reliable, current hazard and road-network data become available.

These extensions would require appropriate data, testing, and validation before being used for real-world safety decisions.

11. CONCLUSION

FloodLens connects AI-assisted pothole detection with structured hazard reporting and geographical hotspot identification. By organizing image-based evidence and location-based reports in one workflow, it aims to make recurring road issues more visible and support more informed inspection priorities.

The central idea is simple: detect hazards, organize reports, identify clusters, and help people make better-informed decisions.

FLOODLENS — DETECT HAZARDS. IDENTIFY HOTSPOTS. ENABLE SMARTER DECISIONS.
