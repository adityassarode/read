Baya

Baya is a structured, production-ready Machine Learning orchestration and AutoML framework designed for clear, reproducible, and extensible ML workflows.

It supports both:

• Minimal one-line training
• Fully modular ML pipelines
• AutoML with leaderboard tracking
• Exporting results to multiple formats

Why Baya?

Multiple abstraction layers (simple → advanced)

Built-in AutoML engine

DAG-based orchestration

Experiment tracking

Model registry

CLI interface

Export system (CSV, JSON, Excel, PDF, DOCX, PNG, etc.)

Fully compatible with Pandas workflows

Extensible and modular architecture

Installation
pip install baya

Runtime dependencies installed automatically:

pandas

numpy

scikit-learn

scipy

pyyaml

matplotlib

Works With Pandas

Baya integrates directly with Pandas.

You can freely mix Pandas + Baya:

import pandas as pd
from baya import quick_train

df = pd.read_csv("data.csv")

# Use pandas normally
df["new_feature"] = df["feature"] * 2

# Pass directly into Baya
metrics = quick_train(
    data=df,
    target="Target",
    model="linear_regression"
)

print(metrics)

You can:

preprocess with pandas

clean manually

engineer features

then hand over to Baya

No restrictions.

API Layers

Baya supports three levels of control.

1️⃣ Simple API — quick_train()

Minimal lines.

from baya import quick_train

metrics = quick_train(
    data="data.csv",
    target="Target",
    model="linear_regression",
    test_size=0.2
)

Supported data inputs:

pandas DataFrame

CSV path

JSON path

Excel path

Automatically performs:

load

target selection

split

model creation

train

predict

evaluate

Returns metrics dictionary.

2️⃣ Fluent API — Baya Class

Chainable interface.

from baya import Baya

metrics = (
    Baya("data.csv", target="Target")
    .train("linear_regression")
    .evaluate()
)

Also works with DataFrame:

Baya(df, target="Target").train("logistic_regression").evaluate()
3️⃣ Advanced API — Project

Full modular control.

from baya import Project

project = Project()

project.data.load("data.csv")
project.data.set_target("Target")

project.split.train_test(test_size=0.2)

project.model.create("linear_regression")
project.model.train()

metrics = project.evaluate.evaluate_regressor()
All Core Methods (Advanced API)

Data:

project.data.load(path_or_dataframe)
project.data.set_target("column")
project.data.preview()

Split:

project.split.train_test(test_size=0.2)

Model:

project.model.create("linear_regression")
project.model.train()
project.model.predict()

Evaluate:

project.evaluate.evaluate_regressor()
project.evaluate.evaluate_classifier()
project.evaluate.custom_metric(...)

Tracking:

project.tracker.start()
project.tracker.log_metrics(...)
project.tracker.finalize()

Export:

project.export.csv("results.csv")
project.export.json("results.json")
project.export.excel("results.xlsx")
project.export.pdf("report.pdf")
project.export.docx("report.docx")
project.export.image("plot.png")
Supported Export Formats

Baya supports exporting to:

.csv

.json

.xlsx

.pdf

.docx

.png

.jpg

Exports available for:

metrics

predictions

leaderboards

visualizations

reports

AutoML

Automatic model selection.

from baya import automl

result = automl(
    data="data.csv",
    target="Target"
)

print(result["best_model"])
print(result["best_score"])

AutoML includes:

Cross-validation

Model comparison

Leaderboard generation

Best model selection

Run tracking

CV results storage

Leaderboard

Stored in:

baya_runs/leaderboard.json

Visualize:

from baya.visualize import plot_leaderboard
plot_leaderboard()
Model Registry
from baya import register_model, list_models

register_model("my_model", MyModelClass)
print(list_models())

Built-in models:

linear_regression

logistic_regression

random_forest_classifier

random_forest_regressor

svm_classifier

svm_regressor

Config-Based Reproducibility

workflow.yaml:

data_path: data.csv
target: Target
model: logistic_regression
task: classification
test_size: 0.2
seed: 42

Run:

from baya import Project

project = Project.from_config("workflow.yaml")
metrics = project.run()
CLI Usage
baya info
baya run workflow.yaml
baya automl workflow.yaml
baya registry list-models
baya leaderboard
baya visualize leaderboard
Task Auto Detection

Automatically detects:

Regression

Classification

Based on target variable.

Architecture

Layered Design:

Core Engine
↓
Orchestration (DAG)
↓
Simple API
↓
AutoML
↓
CLI

Simple API wraps advanced engine — no duplicated logic.

Optional Dependencies

Install extra features:

Visualization extras:

pip install baya[viz]

Deep learning extras:

pip install baya[deep]

Development tools:

pip install baya[dev]
Branding
baya info

Shows:

Framework name

Version

Author

Website

Support link

Branding is non-intrusive.

Developer Setup
git clone <repo>
cd baya
pip install -e .[dev]
pytest
License

MIT License.

About

Baya is built and maintained by Aditya Sarode, focused on scalable AI systems, ML architecture, and production-ready engineering.
