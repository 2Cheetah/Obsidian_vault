# Poetry

## Add libraries
#requirements_txt

If `requirements.txt` file is available, it can be source of dependencies for the poetry project:
```shell
poetry add `cat requirements.txt`
```

## Export
#requirements_txt 

To export poetry required packages list to `requirements.txt`:
```shell
poetry export --format=requirements.txt --without-hashes --output=requirements.txt
```

Output will look like:
```text
cachetools==5.2.1 ; python_version >= "3.10" and python_version < "4.0"
certifi==2022.12.7 ; python_version >= "3.10" and python_version < "4"
charset-normalizer==3.0.1 ; python_version >= "3.10" and python_version < "4"
idna==3.4 ; python_version >= "3.10" and python_version < "4"
requests==2.28.2 ; python_version >= "3.10" and python_version < "4"
urllib3==1.26.14 ; python_version >= "3.10" and python_version < "4"
```

