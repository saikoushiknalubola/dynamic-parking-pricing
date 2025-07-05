project_title: Dynamic Pricing for Urban Parking Lots
program: Summer Analytics 2025 – Capstone Project
hosted_by: Consulting & Analytics Club × Pathway

overview: |
  This project addresses the inefficiencies in urban parking due to static pricing systems.
  It implements a real-time dynamic pricing engine using Python tools to optimize utilization
  across 14 urban parking locations. The system adjusts prices based on real-time demand
  features like occupancy, traffic, queue length, special events, and vehicle type.

tech_stack:
  language: Python
  libraries:
    - NumPy
    - Pandas
    - Pathway
    - Bokeh
    - Panel
  environment: Google Colab

repository_structure:
  - notebook/
      - final_notebook.ipynb: Fully working Colab notebook with Model 1 and Model 2
  - report/
      - Dynamic_Pricing_Report.pdf: Optional PDF report with methodology
  - data/
      - dataset.csv: Sample dataset for manual upload
  - README.md: Main documentation
  - requirements.txt: (optional) environment setup file

architecture_diagram: |
  mermaid:
    graph TD
    A[CSV Dataset] --> B[Pathway Replay Stream]
    B --> C[Feature Engineering]
    C --> D[Model 1: Linear Pricing]
    C --> E[Model 2: Demand-Based Pricing]
    D --> F[Bokeh Visualization]
    E --> F

project_workflow:
  1_data_ingestion:
    - Merge date and time into a timestamp
    - Sort the data by time
    - Stream using Pathway’s replay_csv with input_rate=1000

  2_feature_engineering:
    - Calculate occupancy ratio
    - Derive queue length
    - Simulate traffic level
    - Add event/special day indicator
    - Estimate vehicle type weight

  3_models:
    model_1:
      name: Baseline Linear Pricing
      formula: Price = Base Price + α * (Occupancy / Capacity)
      notes: Basic linear scaling based on demand
    model_2:
      name: Demand-Based Dynamic Pricing
      features_used:
        - Occupancy rate
        - Queue length
        - Traffic congestion
        - Special day indicator
        - Vehicle type weight
      demand_formula: |
        Demand = 0.6*(Occupancy/Capacity)
               + 0.2*QueueLength
               - 0.1*Traffic
               + 0.1*SpecialDay
               + 0.05*VehicleTypeWeight
      pricing_function: Price = Base_Price * (1 + λ * NormalizedDemand)
      bounds: [$5, $20]
    model_3:
      name: Competitive Pricing (Conceptual)
      status: Not implemented (single-location dataset)
      concept: |
        - Use latitude/longitude for proximity detection
        - Compare prices across nearby lots
        - Suggest rerouting or adjust price accordingly

  4_real_time_processing:
    - Streamed using Pathway’s real-time engine
    - Feature computation and pricing logic applied on-the-fly
    - Pipeline runs using pw.run()

  5_visualization:
    tool: Bokeh + Panel
    output: Real-time pricing plots embedded in Colab
    functionality: Interactive time-series visualization of prices

how_to_run:
  prerequisites:
    - Clone the repository
    - Open final_notebook.ipynb in Google Colab
    - Upload dataset.csv manually
    - Run all cells sequentially
  commands:
    - git clone https://github.com/yourusername/dynamic-parking-pricing.git

documentation:
  report: report/Dynamic_Pricing_Report.pdf
  license: Not specified (can be added if needed)
  requirements: requirements.txt (optional for local setup)
  authorship: Submitted by Saikoushik Nalubola (or your name)

reviewer_notes:
  - All required models implemented as per problem statement
  - All code written from scratch using allowed libraries only
  - Notebook runs completely in Colab without error
  - Public access ensured or reviewer access granted

submission_instructions:
  - Ensure this GitHub repo is public or shared with reviewers
  - Submit using the same email ID used during registration
  - README.md includes:
      - Project overview
      - Tech stack
      - Architecture diagram
      - Detailed model explanations
      - Execution instructions
      - Report (optional)

acknowledgments: |
  This project was developed as part of the Summer Analytics 2025 Capstone,
  hosted by the Consulting & Analytics Club in collaboration with Pathway.
