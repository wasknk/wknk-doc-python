# Uvicorn


## basic usage
start on http://127.0.0.1:8000/
```
uvicorn main:app --reload
```

start on http://127.0.0.1:8080/
```
uvicorn main:app --reload --port 8080
```


```
uvicorn main:app --host 0.0.0.0 --port 8000
```