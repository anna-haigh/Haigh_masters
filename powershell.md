# Windows 3.11 + venv + Roboflow Local Inference Cheat Sheet
## Install Python 3.11

Download from Python 3.11 official release
.

Run installer:

Check “Add Python 3.11 to PATH”

Click Customize installation → Install for all users (optional)

Verify in PowerShell:
```
py -3.11 --version
```
Should output: Python 3.11.x

## Create a Virtual Environment

Open PowerShell (do NOT enter Python first).

Navigate to your project folder:

```
cd C:\Users\haigh\roboflow_inference
```

Create venv using Python 3.11:

```
py -3.11 -m venv roboflow_env
```

This creates a folder roboflow_env in your project directory.

## Activate the Virtual Environment
```
.\roboflow_env\Scripts\Activate.ps1
```

Prompt changes to:
```
(roboflow_env) PS C:\Users\haigh\roboflow_inference>
```

Deactivate when done:
```
deactivate
```

## Install Required Packages

With venv activated:
```
pip install inference requests
```

This installs Roboflow offline inference and HTTP request support inside the isolated environment.

## Download & Set Up Your Offline Roboflow Model

Export your trained model from Roboflow as ONNX, TorchScript, or Docker.

Place it in your project folder, e.g.:
```
C:\Users\haigh\roboflow_inference\model\
```

If using Docker:
```
docker run -it -p 9001:9001 -v C:\Users\haigh\roboflow_inference\model:/model roboflow/inference-server-cpu:latest --model /model/model.onnx
```

If using Python directly:
```
from inference import get_model

model = get_model("C:\\Users\\haigh\\roboflow_inference\\model\\model.onnx")
result = model.infer("test.jpg")
print(result)
```
## Test the Setup

Place an image in your folder (e.g., test.jpg).

Run Python inside venv:

python


Test inference:
```
from inference import get_model

model = get_model("C:\\Users\\haigh\\roboflow_inference\\model\\model.onnx")
result = model.infer("test.jpg")
print(result)
```

## Tips

Always activate venv before installing packages or running scripts.

Use py -3.11 script.py to ensure scripts run with Python 3.11.

Use deactivate to leave the venv.

For Docker offline inference, 
