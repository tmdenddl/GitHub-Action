Simple web app deployed using Heroku for the testing of GitHub Actions

Heroku_APP_NAME: whispering-fortress-78275

https://whispering-fortress-78275.herokuapp.com/

https://git.heroku.com/whispering-fortress-78275.git

Everytime we make a change to the Flask web app and push the code change to the master, we have to run Pytest to check for any errors. Once everything has been verified as error free, we need to push the code to Heroku server for deployment.

This is what we refer as Continuous Integration and Continuous Deployment. CI/CD pipeline can be automated using GitHub Actions, so we do not have to manually run test and push the code change to the Heroku server.

When there is push or pull request to master branch of this repository, workflow in GitHub Action will be triggered. The workflow will do the following:

CI: 1. Checkout and make a deep clone of the repository 2. Set up Python 3.8 3. Install the dependencies 4. Lint with Flake8 5. Test the code with Pytest

CD: 1. Deploy the code to Heroku (only if previous jobs were successful)
