---
title: "ViewComfy API Integration Guidelines"
description: "You are an expert in Python, FastAPI integrations, and web app development. Your role involves integrating the ViewComfy API into web applications using Python."
category: "rules"
tags: ["Python", "FastAPI", "API Integration", "Web Development"]
tech_stack: ["FastAPI", "httpx", "JSON"]
---

You are an expert in Python, FastAPI integrations, and web app development. Your role involves integrating the ViewComfy API into web applications using Python.

### Overview of the ViewComfy API
The **ViewComfy API** is a serverless API built on the **FastAPI** framework, designed to execute custom **ComfyUI** workflows. When using Python, you will make requests through the **httpx** library.

### Important Considerations
- **Cold Start**: The first invocation of the API may experience a cold start, leading to longer response times.
- **Variable Generation Times**: Execution times can differ significantly; some workflows may complete in under 2 seconds, while others could take several minutes.

### API Request Guidelines
- **Parameters Object**: Ensure that the `params` object is not empty. If no specific parameters are provided, modify the seed value.

### Response Format
The API returns data in the following JSON structure:

```json
{
  "prompt_id": "string", // Unique identifier for the prompt
  "status": "string", // Current execution status
  "completed": bool, // Indicates if execution is complete
  "execution_time_seconds": float, // Time taken to execute
  "prompt": dict, // Original prompt configuration
  "outputs": [ // List of output files (optional)
    {
      "filename": "string", // Name of the output file
      "content_type": "string", // MIME type of the file
      "data": "string", // Base64 encoded file content
      "size": int // File size in bytes
    }
  ]
}
```

### Steps to Integrate the ViewComfy API

#### 1. Deploy Your Workflow
Begin by deploying your ComfyUI workflow on the ViewComfy dashboard using the `workflow_api.json` file.

#### 2. Calling the Workflow with the API
The ViewComfy API can be accessed via a standard POST request and supports streaming responses through **Server-Sent Events**. This allows for real-time tracking of **ComfyUI** logs.

#### 3. Obtain Your API Keys
To use the API endpoint, generate your API keys from the ViewComfy dashboard.

#### 4. Extract Workflow Parameters
Identify the parameters in your workflow using the `ViewComfy_API/Python/workflow_parameters_maker.py` script. This script flattens your `workflow_api.json`.

The flattened JSON file should resemble the following structure:

```json
{
  "_3-node-class_type-info": "KSampler",
  "3-inputs-cfg": 6,
  "_6-node-class_type-info": "CLIP Text Encode (Positive Prompt)",
  "6-inputs-clip": [ "38", 0 ],
  "6-inputs-text": "A woman raising her head with hair blowing in the wind",
  "_52-node-class_type-info": "Load Image",
  "52-inputs-image": "<path_to_my_image>"
}
```

In this example, the first key-value pair indicates that node 3 is the **KSampler**, and the `"3-inputs-cfg"` key sets its corresponding configuration value.

#### 5. Update Your Script with Parameters
Copy the ViewComfy endpoint from your dashboard and assign it to `view_comfy_api_url`. Retrieve your **Client ID** and **Client Secret**, and set them as follows:

```python
view_comfy_api_url = "<Your_ViewComfy_endpoint>"
client_id = "<Your_ViewComfy_client_id>"
client_secret = "<Your_ViewComfy_client_secret>"
```

Next, set the parameters using the keys from the flattened JSON file. For instance, to modify the prompt and input image, do the following:

```python
params = {}
params["6-inputs-text"] = "A flamingo dancing on top of a server in a pink universe, masterpiece, best quality, very aesthetic"
params["52-inputs-image"] = open("/home/gbieler/GitHub/API_tests/input_img.png", "rb")
```

#### 6. Calling the API
Once you have added your parameters to `ViewComfy_API/Python/main.py`, execute the API call by running:

```bash
python main.py
```

This command sends your parameters to `ViewComfy_API/Python/api.py`, where the functions for API calls and output handling are defined.

- The script defaults to the `infer_with_logs` function, which streams generation logs from **ComfyUI**. If you prefer a standard POST request, use the `infer` function instead.

The returned result object will include both the workflow outputs and generation details, with outputs automatically saved in your working directory.

### API Functionality Overview
The API file (`api.py`) contains functions to interact with the API and manage responses. The main file (`main.py`) is typically the only file you need to modify for your specific workflow.

#### API Endpoints
- **infer**: A classic request-response endpoint that waits for the request to complete before returning results.
- **infer_with_logs**: Provides real-time updates with **ComfyUI** logs (e.g., progress bar). To utilize this endpoint, pass a function that handles incoming log messages.

### Extracting API Parameters
To extract all parameters from your `workflow_api.json`, invoke the `workflow_api_parameter_creator` function. This will generate a dictionary containing all parameters within the workflow.