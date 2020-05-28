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
#### Change the requirements file
#### ----requirements.txt---- ####
```
flask
pytest
```
#### ------------------------ ####

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
#### ----app.py---- ####
```
from flask import Flask

app = Flask(__name__)

@app.route("/")
def index():
    return "Hello, World!"

if __name__ == "__main__":
    app.run()
```
#### ---------------- ####

#### Make test directory and test file
```
cd ..
mkdir tests
cd tests
touch test_app.py
vim test_app.py
```
#### ----test_app.py---- ####
```
from app import index

def test_index():
    assert index() == "Hello, World!"
```
#### ------------------- ####

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
#### ----.gitignore---- ####
```
/myvenv
__pycache__/
```
#### ------------------ ####

#### Setting up Actions

##### 1. Go to Actions Tab
##### 2. Set up "Python application" Workflow
##### 3. Then add, 'export PYTHONPATH=src' on the workflow file at 'Test with pytest' stage
##### 4. This should successfully run the CI workflow

#### Setting up Heroku

##### 1. Go to Heroku website, make an account
##### 2. Download Heroku CLI using brew commands
```
brew tap heroku/brew && brew install heroku
```

#### How to deploy the web app to Heroku server
##### 1. Login to Heroku CLI and create app
```
heroku login
heroku create
```
```
https://shielded-chamber-49557.herokuapp.com/ | https://git.heroku.com/shielded-chamber-49557.git
```
##### 2. Push the code to Heroku server
```
git push heroku master
```
##### 3. We don't want to run push everytime there is a code change in git, use Action to automated the deployment

#### How to use Action to automate the deployment

##### 1. Create a Heroku token by running:
```
heroku authorizations:create
```
##### 2. Go to Settings > Secrets, then save the token into Secret storage
```
Name: HEROKU_API_TOKEN
Value: TOKEN_VALUE
```
##### 3. In the Secret storage, also add HEROKU_APP_NAME
```
Name: HEROKU_APP_NAME
Value: shielded-chamber-49557
```
##### 3. Go to workflow file and add the following to as a new step
```
    - name: Deploy to Heroku
    env:
      HEROKU_API_TOKEN: ${{ secrets.HEROKU_API_TOKEN }}
      HEROKU_APP_NAME: ${{ secrets.HEROKU_APP_NAME }}
    if: github.ref == 'refs/heads/master' && job.status == 'success'
    run: |
      git remote add heroku https://heroku:$HEROKU_API_TOKEN@git.heroku.com/$HEROKU_APP_NAME.git
      git push heroku HEAD:master -f
``` 
##### 4. Create Procfile in the repository
```
vim Procfile
```

```
web gunicorn --pythonpath src app:app
```
##### 5. Create runtime.txt in the repository
```
vim runtime.txt
```

```
python-3.7.6
```
##### 6. In the requirements.txt add gunicorn
##### 7. Add the following to checkout Action job:
```
run: |
      git fetch --prune --unshallow
```
