# GitHub-Action
For demo on how the CI/CD pipeline works on GitHub Action

#### Remove the username in terminal
```
S1="$: "
```
#### Activate Python3 virtual environment
```
python3 -m venv myvenv
source myvenv/bin/activate
```
#### Install Flask and Pytest
```
pip install flask pytest
```
#### Create a requirement.txt file with all the dependencies inside
```
pip freeze > requirements.txt
```
#### Make src repository
```
mkdir src
cd src
```
#### Make app.py file
```
touch app.py
vim app.py
```
#### app.py ##
```
from flask import Flask

app = Flask(__name__)

@app.route("/")
def index():
    return "Hello, World!"

if __name__ == "__main__":
    app.run()
```
#### end of app.py

#### Make test directory and test file
```
cd ..
mkdir tests
cd tests
touch test_app.py
vim test_app.py
```
#### test_app.py
```
from app import index

def test_index():
    assert index() == "Hello, World!"
```
#### end of test_app.py

#### Set PYTHONPATH so src directory can be referenced
```
export PYTHONPATH=src
```
#### Move back to root directory and run test
```
cd ..
pytest
```
#### Create .gitignore file
```
vim .gitignore
```
#### .gitignore ##
```
/myvenv
__pycache__/
```
#### end of .gitignore
