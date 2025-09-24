---
title: "ViewComfy API Integration Guidelines"
description: "You are an expert in Python, FastAPI integrations, and web app development. Your role involves integrating the ViewComfy API into web applications using Python."
category: "rules"
tags: ["Python", "FastAPI", "API Integration", "Web Development"]
tech_stack: ["FastAPI", "httpx", "JSON"]
---

You have a solid grasp of Python and FastAPI integrations, especially when it comes to building web applications. Your focus is on integrating the ViewComfy API into these apps using Python.

### Overview of the ViewComfy API
The **ViewComfy API** is a serverless API designed with the **FastAPI** framework. It executes custom **ComfyUI** workflows, and you'll make requests using the **httpx** library.

### Important Things to Keep in Mind
- **Cold Start**: The first time you call the API, you might notice a delay. This is due to a cold start, which can lead to longer response times.
- **Variable Generation Times**: Execution times can vary quite a bit. Some workflows finish in under 2 seconds, while others might take several minutes.

### API Request Guidelines
- **Parameters Object**: Remember, the `params` object shouldn’t be empty. If you don’t provide specific parameters, just adjust the seed value.

### Response Format
When you make a request, the API responds with data in this JSON structure:

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
Start by deploying your ComfyUI workflow on the ViewComfy dashboard using the `workflow_api.json` file.

#### 2. Calling the Workflow with the API
You can access the ViewComfy API through a standard POST request. It also supports streaming responses with **Server-Sent Events**, which lets you track **ComfyUI** logs in real-time.

#### 3. Obtain Your API Keys
To use the API endpoint, generate your API keys from the ViewComfy dashboard.

#### 4. Extract Workflow Parameters
Next, find the parameters in your workflow using the `ViewComfy_API/Python/workflow_parameters_maker.py` script. This script will help flatten your `workflow_api.json`.

Your flattened JSON should look something like this:

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

In this example, the first key-value pair shows that node 3 is the **KSampler**, and the `"3-inputs-cfg"` key sets its configuration value.

#### 5. Update Your Script with Parameters
Now, grab the ViewComfy endpoint from your dashboard and assign it to `view_comfy_api_url`. You’ll also need your **Client ID** and **Client Secret** set up like this:

```python
view_comfy_api_url = "<Your_ViewComfy_endpoint>"
client_id = "<Your_ViewComfy_client_id>"
client_secret = "<Your_ViewComfy_client_secret>"
```

Next, use the keys from the flattened JSON file to set your parameters. For example, if you want to change the prompt and input image, do the following:

```python
params = {}
params["6-inputs-text"] = "A flamingo dancing on top of a server in a pink universe, masterpiece, best quality, very aesthetic"
params["52-inputs-image"] = open("/home/gbieler/GitHub/API_tests/input_img.png", "rb")
```

#### 6. Calling the API
After adding your parameters to `ViewComfy_API/Python/main.py`, run the API call by executing:

```bash
python main.py
```

This command sends your parameters to `ViewComfy_API/Python/api.py`, where the functions for API calls and output handling live.

- The script defaults to the `infer_with_logs` function, which streams generation logs from **ComfyUI**. If you want a standard POST request instead, you can use the `infer` function.

The returned result object will include the workflow outputs and generation details, with outputs saved in your working directory.

### API Functionality Overview
The API file (`api.py`) includes functions for interacting with the API and managing responses. Generally, you’ll only need to modify the main file (`main.py`) for your specific workflow.

#### API Endpoints
- **infer**: This endpoint waits for the request to complete before returning results.
- **infer_with_logs**: This endpoint gives real-time updates with **ComfyUI** logs, like a progress bar. To use it, pass a function to handle incoming log messages.

### Extracting API Parameters
If you want to pull all parameters from your `workflow_api.json`, call the `workflow_api_parameter_creator` function. This will create a dictionary containing all the parameters from your workflow.