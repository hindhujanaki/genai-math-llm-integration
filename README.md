

## Integration of a Mathematical Calulations with a Chat Completion System using LLM Function-Calling

### AIM:
To design and implement a Python function for calculating the volume of a cylinder, integrate it with a chat completion system utilizing the function-calling feature of a large language model (LLM).

### PROBLEM STATEMENT:

Enhancing mathematical problem-solving capabilities in educational platforms by integrating Generative AI (Large Language Models) with symbolic computation tools to provide accurate, step-by-step solutions and improve student learning outcomes.

### DESIGN STEPS:

STEP 1:
Import necessary libraries, including OpenAI for LLM integration and math for mathematical operations.

STEP 2:
Define a Python function to calculate the volume of a cylinder based on its radius and height.

STEP 3:
Integrate the function into an LLM-based chat completion system with function-calling capabilities.

### PROGRAM:

```
import openai
import json
import math

def calculate_cylinder_volume(radius: float, height: float) -> float:
    """Calculate the volume of a cylinder."""
    return math.pi * radius**2 * height

# Define available functions for the LLM
functions = [
    {
        "name": "calculate_cylinder_volume",
        "description": "Calculate the volume of a cylinder given radius and height.",
        "parameters": {
            "type": "object",
            "properties": {
                "radius": {"type": "number", "description": "Radius of the cylinder."},
                "height": {"type": "number", "description": "Height of the cylinder."}
            },
            "required": ["radius", "height"]
        }
    }
]

# Function to handle chat completion with function calling
def chat_with_function(user_input: str):
    response = openai.ChatCompletion.create(
        model="gpt-4-1106-preview",  # Ensure this is a function-calling supported model
        messages=[{"role": "user", "content": user_input}],
        functions=functions,
        function_call="auto"  # Let the model decide if function calling is needed
    )
    
    message = response["choices"][0]["message"]
    if message.get("function_call"):
        function_name = message["function_call"]["name"]
        arguments = json.loads(message["function_call"]["arguments"])
        
        if function_name == "calculate_cylinder_volume":
            result = calculate_cylinder_volume(**arguments)
            return f"The volume of the cylinder is {result:.2f} cubic units."
    
    return message.get("content", "I couldn't process your request.")

# Example usage
if __name__ == "__main__":
    radius = float(input("Enter the radius of the cylinder: "))
    height = float(input("Enter the height of the cylinder: "))
    user_query = f"What is the volume of a cylinder with radius {radius} and height {height}?"
    print(chat_with_function(user_query))


```


### OUTPUT:

![image](https://github.com/user-attachments/assets/c44e90e1-99e0-4c07-91f0-97f33328e8c8)


### RESULT:
Hence,the python program to design and implement a Python function for calculating the volume of a cylinder, integrating it with a chat completion system utilizing the function-calling feature of a large language model (LLM) is successfully demonstrated.




