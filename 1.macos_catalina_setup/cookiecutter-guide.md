# Cookiecutter Training

* This repository was created to guide me through my learning experience with Cookiecutter

------------------------------------------------------

### Cookiecutter philosophy

> Provides a command-line utility that creates projects from cookiecutter.

### 1. Create my environment

+ Navigate to:
    ```shell script
    $cd /Users/fcp/workspace/1.git/cookiecutter
    ```

+ Create a python environment
    ```shell script
    $conda create --prefix ./env python
    ```

+ Configure Pycharm to use: `/Users/fcp/workspace/1.git/cookiecutter/env/bin/python`

### 2. Installing Cookiecutter

+ Activate your conda env
    ```shell script
    $conda activate env/
    ```

+ On terminal, type:
    ```shell script
    $pip3 install --user cookiecutter
    
    # or use conda
    $conda config --add channels conda-forge
    $conda install cookiecutter 
    ```
+ Check installation 
    ```shell script
    $conda list
    ```

### 3. Using a random cookiecutter template

+ On your cookiecutter folder, type:
    ```shell script
    $cookiecutter https://github.com/avelino/cookiecutter-bottle
    ```
    > Answer the questions

+ Install requirements
    ```shell script
    $pip install -r requirements.txt
    ```
+ Run the test
    ```shell script
    $python manage.py runserver
    ```
    > Now you are able to test the  http://0.0.0.0:8080/

+ Check the location of all you cookiecutter clones
    ```shell script
    $ls /Users/fcp/.cookiecutters/
    ```

### 4. Some tips

1. You can use the following command to avoid cookiecutter question

    ```shell script
    $cookiecutter TEMPLATE --no-input  #change template!
    ```

2. You can have a default configure file to answer all the questions

    + On your cookiecutter project folder, create the following
    ```shell script
    $touch /Users/fcp/workspace/1.git/cookiecutter/defaults-fcp.yaml
    ```
    
    + Open and edit the file:
    ```shell script
    $vi defaults-fcp.yaml
    ```

    ```yaml
    default_context:
        full_name: "Fernando Carvalho Pacheco"
        email: "fernando.pacheco@hawaii.edu"
        github_username: "fcarvalhopacheco"

    ```

    + run the following:
    ```shell script
    $cookiecutter cookiecutter-bottle --config-file /Users/fcp/workspace/1.git/cookiecutter/defaults-fcp.yaml
    ```

3. Use Replay

+ The following command will re-do last commands. 
    ```shell script
    $cookiecutter cookiecutter-bottle --replay
    ```
    > the code typed before is stored here ~/.cookiecutter_replay/cookiecutter-bottle.json


### 5. Creating your own templates

+ Decrease friction on projects you often use
+ Empower your team and assist new developers
+ Ease adoption of your open source project


1. On your cookiecutter projects folder, create a new folder

    ```shell script
    $mkdir {{cookiecutter.cruise_number}}
    ```

2. create a .jon file

    ```shell script
    $touch cookiecutter.json
    ```

3. Create files inside {{cookiecutter.cruise_number}}

    ```shell script
    $cd {{cookiecutter.cruise_number}}
    $touch README.md
    $touch history.{{cookiecutter.cruise_number}}
    ```

4. edit cookiecutter.json

    ```shell script
    $cd ..
    $vi cookiecutter.json 
    ```

    + add the following 

    ```json
    {
      "cruise_number": "400",
      "cruise_date_start": "YYYY-MM-DD ",
      "cruise_date_end": "YYYY-MM-DD",
      "chief_scientist": "Chief Scientist name",
      "creator": "Your name"
    }
    ```

5. edit history.{{cookiecutter.cruise_number}}

    ```shell script
    $cd {{cookiecutter.cruise_number}}
    $vi history{{cookiecutter.cruise_number}}
    ```

    + add the following

    ```text
    Cruise: HOT-{{cookiecutter.cruise_number}}

    Dates: Start:{{cookiecutter.cruise_date_start}}
             End:{{cookiecutter.cruise_date_start}}

    Chief Scientist: {{cookiecutter.chief_scientist}}
    ```

6. edit README.md

    ```shell script
    $vi README.md
    ```

    + add the following:

    ```markdown
    # Project: {{cookiecutter.cruise_number}}

    Cruise: HOT-{{cookiecutter.cruise_number}}

    Dates: Start:{{cookiecutter.cruise_date_start}}
             End:{{cookiecutter.cruise_date_start}}

    Chief Scientist: {{cookiecutter.chief_scientist}}
    ```

7. Test your template

    + on your folder:  /Users/fcp/workspace/1.git/cookiecutter/, type

    ```shell script
    $cookiecutter /Users/fcp/workspace/1.git/cookiecutter/cookiecutter-hot
    ```
    > you should able to answer the questions from your .json file

8. Working with dependent values

    + On your `cookiecutter.json` file, add the following:
    
    ```yaml
    {
      "cruise_number": "400",
      "cruise_date_start": "YYYY-MM-DD",
      "cruise_date_end": "YYYY-MM-DD",
      "chief_scientist": "Chief Scientist name",
      "creator": "Your name",                         #DON'T INCLUDE THE BELOW NOTE  
      "created_on": "{% now 'local' %}"      <----- NOTE, this is a pypi extension
                                                      to show today's date
    }
    ```
   
   + Now let's create `required` inputs
   + On your `cookiecutter.json` file, add the following:
        > this is just an example and will not be created

    ```yaml   
    {
      "cruise_number": "400",
      "cruise_date_start": "YYYY-MM-DD",
      "cruise_date_end": "YYYY-MM-DD",
      "chief_scientist": "Chief Scientist name",
      "creator": "Your name",
      "created_on": "{% now 'local' %}"
      
     # The following is a python list of string that requires user selection!
     # On this case: 1 or 2 
      "cruise_vessel": ["Kilo-Moana","Oscar-Settle"] 
    }
    ```
   
9. Working with hooks, codes to be run after the template creation
    
    + on top level folder  `Users/fcp/workspace/1.git/cookiecutter/cookiecutter-hot`
      create the following:
    
    ```shell script
    $mkdir hooks
    %touch pre_gen_project.py
    %vi pre_gen_project.py
    ```
   + add the following:
   
   ```python
   import sys

    def validate():
        creator = '{{cookiecutter.creator}}'

        if not creator.strip():
            print("ERROR FAILED(1): You must specify a creator to use this template")
            return 1

        if creator.lower().strip() == 'your name':
            print("ERROR FAILED(2): You must specify a creator to use this template")
            return 2

        return 0


    if __name__ == '__main__':
        sys.exit(validate())  
   ```
   
    
