# FastAPI

Specialized framework for (fast) creating a HTTP - API using Python.

It uses Python decorators and Pydantic data models

It also generate OpenAPI documentation. (SwaggerUI)

## Minimal requirements

Virtual Python enviroment with fastAPI package:

````bash
#requirements.txt:
fastapi[standard]

# Create and install:
python -m venv .venv && pip install -r requirements.txt
````

It comes with a 

## Main definitions & Hello world app

This is the minial fastAPI functionality:
````python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():
    return {"msg": "hello world"}
````

The fastAPI project is launched using `fastapi dev main.py`

The FastAPI object contains:
* Routes
* Configurations
* Validation
* API Documentation

The home function is the definition of the endpoint, using the python decorator. FastAPI will convert the Python dicts into JSON automatically (using serialization)

### Routes
The definition of the API can define variables to be used in the Python method and tune the response of that endpoint:

````python
@app.get("/wines")
def get_wines():
    return {"wines": []}

@app.get("/wines-limit")
def get_wines_with_limit(limit: int = 10):
    return {"wines": [], "limit": limit}

@app.get("/wines/{wine_id}")
def get_wine(wine_id: int):
    return None
````

Adding the type hint in the method definition automatically adds a FastAPI validation.

Parameters can be defined only in the python method to define query parameters

### Schemas
Adding hint types of `pydantinc.BaseModel` makes the FastAPI able to validate Api calls of that defined type:

````python
# schemas.py
from pydantic import BaseModel

class Wine(BaseModel):
    name: str
    description: str | None = None
    price: float

#main.py    
@app.post("/wines", status_code=201)
def create_wine(wine: Wine):
    return wine
````

Validations can be override by the user also:
````python
from pydantic import BaseModel, Field

class Wine(BaseModel):
    name: str = Field(min_length=3)
    description: str | None = None
    price: float = Field(gt=0)
````

#### CRUD: Create, Read, Update and Delete

Complete CRUD routes for the wine example:

````python
from fastapi import FastAPI
from schemas import Wine


app = FastAPI()

wines: dict[int, Wine] = {}

@app.get("/")
def home():
    return {"msg": "hello world"}


@app.get("/wines")
def get_wines(limit: int = 10):
    return list(wines.values())[:limit]

@app.get("/wines/{wine_id}")
def get_wine(wine_id: int):
    return wines.get(wine_id)

@app.post("/wines", status_code=201)
def create_wine(wine: Wine):
    wine.id = len(wines)
    wines[len(wines)] = wine
    return wine

@app.delete("wines/{wine_ide}")
def remove_wine(wine_id: int):
    return wines.pop(wine_id, None)
````

#### Error Management 
Raising exceptions in the routes definion updates the behaviour of FastAPI. In the example, if the wine_id is not found a 404 status code is returned:

````python

@app.delete("wines/{wine_ide}")
def remove_wine(wine_id: int):
    w = wines.pop(wine_id, None)
    if not w:
        raise HTTPException(
            status_code=404,
            detail="Wine not found"
        )
````

#### Routers
FastAPI provides a easy way to tidy-up the source code: The routers

A router groups endpoints in a maintanible and sorted way.

````python
# routers/wines.py
router = APIRouter(
    prefix="/wines",
    tags=["wines"]
)

@router.get("/")
def get_wines(limit: int = 10):
    return list(storage.wines.values())[:limit]

@router.get("/{wine_id}")
def get_wine(wine_id: int):
    w =  storage.wines.get(wine_id, None)
    if not w:
        raise HTTPException(
            status_code=404,
            detail="Wine not found"
        )

@router.post("/", status_code=201)
def create_wine(wine: Wine):
    wine.id = len(storage.wines)
    storage.wines[len(storage.wines)] = wine
    return wine

@router.delete("/{wine_ide}")
def remove_wine(wine_id: int):
    w = storage.wines.pop(wine_id, None)
    if not w:
        raise HTTPException(
            status_code=404,
            detail="Wine not found"
        )

# main.py:
from routers.wines import router as wine_router

#...
app.include_router(wine_router)

````
In the example, now the endpoints have the common prefix of wine hidden inside the router. The main fastAPI requires to register the router in the initialization.