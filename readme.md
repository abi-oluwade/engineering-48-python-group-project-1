# Python Web Scraper App

Aim of the project was to setup a web scrapper app that was provided to us
and create 3 separate environments using the tool stack we have built up so far:
- Development environment
- Testing environment
- Production environment.

This was all achieved using tools such as:
1. Chef =  configuration management tool and sets up the machine and can provision
 it (e.g recipes, metadata, berks_cookbook, unit and spec tests, kitchen.yml and more)

2. Packer = Used to create immutable images of a machine/system.

3. Vagrant and Virtualbox = Used to allow a development environment to be spun up
that allows the devlopers to play around with any changes they have made to the code
locally.

4. Jenkins = An automation server that can listen to the repository that had the
project on it, pull the code when it notices any changes have been made and test
the code on a slave node which was crated by myself that only consisted of the dependencies
and python environment needed on the EC2 instance. Jenkins was then used to merge
the dev3 branch with the master branch of the repo ONLY IF the tests were passed on
the testing slave node. Jenkins also gave feedback via email for any tests triggered and would
give feedback in the event of a failed or passed tests.

# Task 1
## Create a development environment using Vagrant and provision it with Chef such that it can run the application successfully.
The initial task was to set up a development environment that consisted of the application that could successfully be ran, as well as pass the accompanied test that were run using:
````
python3 -m pyests \tests
````
This meant setting up a vagrant file that has the that could simply run 'vagrant up' and initiate the environment
with all the required dependencies and libraries installed.

The development environment was configured with a combination of the vagrant file and a chef cookbook that was created by myself to setup the python environment and the application. Vagrant is able to do this with the provisioner that specifies the tool "chef-solo" and the recipe in the cookbook "devenv"

# Task 2
## Create a testing environment using packer that can create an immutable image of the machine, with the dependencies and the libraries but NOT the application

This was achieved using packer and the chef cookbook in order to again have all the necessary requirements installed but this time NOT have the app included in the image, this was so the app in the repo could be run on the slave node instance on Jenkins for the CI part of the pipeline.

# Task 3
## Setting up a CI pipeline

 Set up a Jenkins CI pipeline that listens to the repo, and if a change is committed pulls the app/code from the repo, tests the app/code on the slave node instance which holds the testing environment and if the tests pass on the slave node, merge the dev3 branch with the master.

# Task 4
## Create a production environment image that can be deployed on an EC2 instance and accessed via the internet

The final stage was a manual creation of the production environment image that mirrored continuous delivery, as after the tests were passed and merged with master, locally the old code was deleted and replaced with the new changed code, the contents of the berks_cookbook was deleted and "berks vendor" and "berks_install" was used to update the cookbook which was used with packer to create a new production environment image AMI that is then deployed onto an EC2 instance.
