# Task 1
## Create a development environment using Vagrant and provision it with Chef such that it can run the application successfully.
The initial task was to set up a development environment that consisted of the application that could successfully be ran, as well as pass the accompanied test that were run using:
````
python3 -m pyests \tests
````
This meant setting up a vagrant file that has the that could simply run 'vagrant up' and initiate the environment
with all the required dependencies and libraries installed. As the code must be included with the development environment the easiest way to install these dependencies was to use the 
