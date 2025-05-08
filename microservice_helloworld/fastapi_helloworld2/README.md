# Hello world with Fastapi

1. poetry new fastapi_helloworld2
2. Select your project with VScode
3. open file pyproject.toml

 [project]
name = "fastapi-helloworld2"
version = "0.1.0"
description = ""
authors = [
    {name = "IBRAR HUSSAIN",email = "ibrar.ali69.ia@gmail.com"}
]
readme = "README.md"
requires-python = ">=3.12"
dependencies = [
    "fastapi (>=0.115.12,<0.116.0)",
    "uvicorn[standard] (>=0.34.2,<0.35.0)",
    "pytest (>=8.3.5,<9.0.0)"
]

[tool.poetry]
packages = [{include = "fastapi_helloworld2", from = "src"}]


[build-system]
requires = ["poetry-core>=2.0.0,<3.0.0"]
build-backend = "poetry.core.masonry.api"

5. install new packages in poetry project poetry add fastapi "uivcorn[standard]"
requires-python = ">=3.12"
dependencies = [
    "fastapi (>=0.115.12,<0.116.0)",
    "uvicorn[standard] (>=0.34.2,<0.35.0)"]
    "pytest (>=8.3.5,<9.0.0)"

6. create main.py location fastapi_helloworld2\main.py
from fastapi import FastAPI


app  = FastAPI()

@app.get("/")
def index():
    return {"Hello": "world"}

@app.get("/piaic/")
def piaic():
    return {"organization": "piaic"}

7. run server poetry run uvicorn fastapi_helloworld2.main:app --reload

 http://127.0.0.1:8000/

8. http://127.0.0.1:8000/piaic/
http://127.0.0.1:8000/docs

9. write your own test
tests\test_main.py

from fastapi.testclient import TestClient
from fastapi_helloworld2.main import app


def test_root_path():
    client = TestClient(app=app)
    response = client.get("/")
    assert response.status_code == 200
    assert response.json() == {"Hello": "world"}

def test_piaic_description():
    client = TestClient(app=app)
    response = client.get("/piaic/")
    assert response.status_code == 200
    assert response.json() == {"organization": "piaic"}

def test_third_check():
    client = TestClient(app=app)
    response = client.get("/piaic/")
    assert response.status_code == 200
    assert response.json() == {"organization": "piaic"}

    10. poetry run test -v