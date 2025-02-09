# The Lightweight Dialogue Game framework

## How to add a new model as a backend

The backend is responsible for calling local or remote models (via an API). You can easily extend clembench with your own models.

1. Add a file that ends in `_api.py` in the backends directory e.g. `mybackend_api.py`
2. Implement in that file your backend class which needs to extend `backends.Backend` e.g. `class MyBackend(backends.Backend)`
3. Add an entry for your backend in the `key.json`

The framework will automatically look into the backends folder for all files that end in `_api.py`
and load all classes in these modules that extend `backends.Backend`.

***Important***: All backends must return a ```prompt, response, response_text``` tuple which must be exactly this:

- ```prompt``` is the exact object that was passed to the LLM (if the object has more structure, keep it as is, do not return only the message string)
- ```response``` is the exact object that was returns by the LLM (again, do not change this object in any way)
- ```response_text``` is only the message generated by the LLM as a string

The first two should get logged into the ```requests.json``` file generated by the game master and should be used for inspection that the actual inputs and outputs are correct. 
