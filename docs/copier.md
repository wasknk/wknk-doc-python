# Copier: Python Project Template Utility 

A powerful command-line tool for generating new Python projects from existing boilerplate templates.

---

### ⚠️ Security Warning ⚠️

**Templates are executable code.** If you use a template from an untrusted or malicious source, it could potentially run arbitrary code on your machine during application. Always ensure your templates originate from a trusted source.

## basic usage 

### install 
```
pipx install copier
# or
uv tool install copier
```

### copy template 

``` 
copier copy https://github.com/my-user-name/my-example-copier.git path/to/destination
```