# Introduction

JSON schemas for dVRK configuration files.  We also provide a small python script to check configuration files against schemas.  The custom script adds a couple of features compared to the default `jsonschema` command:
  * Allow comments in the configuration file.  Internally comments are stripped using `jsmin`.
  * Check the syntax of both JSON files (configuration file and schema) using `json.load`.  Without this, incorrect JSON files are rejected without any useful error message.

Ideally, the C++ code should use the schemas to check the configuration files.  Unfortunately, the C++ library we use to parse JSON files doesn't support JSON schemas (yet).  So for now, the best approach is to test your configuration files as a separate step.

# Requirements

For Python 3:
```sh
sudo apt install python3-jsonschema python3-jsmin
```

For Python 2:
```sh
sudo apt install python-jsonschema python-jsmin
```

# Using the script

Assuming your working directory is the *dVRK* `share/schemas`:
```sh
./json-schema.py -f ../jhu-dVRK/console-MTML-PSM1-Teleop.json -s console.schema.json
```

The output is the Python stack if any error is found.  You will need to read it all to figure out the issue.  If there are not issues found, the scripts outputs **All good**.

# Generate markdown documentation from schemas

* Installation: This is for the dVRK maintainers only.  The tool `jsonschema2md` is available with Python3 only and with pip3 (no Ubuntu package on 18.04):
    ```sh
pip3 install jsonschema2md
```

* Usage:
    ```sh
jsonschema2md console.schema.json console.schema.json.md
```