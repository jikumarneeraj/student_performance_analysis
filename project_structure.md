open terminal ->> create envoriment    ->>>  conda create -p venv python==3.8 -y
for activation ->>> conda activate venv
Create README.md and gitignore file
link to github
create setup.py and requirements.txt

code for setup.py

from setuptools import find_packages,setup
from typing import List


HYPEN_E_DOT='-e .'
def get_requirements(file_path:str)->List[str]:
    '''
    this function will return the list of requirements
    '''
    requirements=[]
    with open (file_path) as file_obj:
        requirements=file_obj.readlines()
        requirements=[req.replace("\n","") for req in requirements]

        if HYPEN_E_DOT in requirements:
            requirements.remove(HYPEN_E_DOT)
    
        return requirements

setup(
    name="Student_analysis",
    version="0.0.1",
    author="Neeraj",
    author_email="neerajkumar1092005@gmail.com",
    packages=find_packages(),
    install_requires=get_requirements('requirements.txt')
)




create ->> src ->> __init__.py
in readme file add "-e ." in the last


create src-> components ->
__init__.py
data_ingestion.py
data_transformation.py
model_trainer.py

create src -> pipeline
__init__.py
train_pipeline.py
predict_pipeline.py

create src -> logger.py,exception.py,utils.py

write exception.py code

import sys
from src.logger import logging

def error_message_detail(error,error_detail:sys):
    _,_,exc_tb=error_detail.exc_info()
    file_name=exc_tb.tb_frame.f_code.co_filename
    error_message="Error occured in python script name [{0}] line number [{1}] error message[{2}]".format(
     file_name,exc_tb.tb_lineno,str(error))

    return error_message

    

class CustomException(Exception):
    def __init__(self,error_message,error_detail:sys):
        super().__init__(error_message)
        self.error_message=error_message_detail(error_message,error_detail=error_detail)
    
    def __str__(self):
        return self.error_message
    


write logger.py code

import logging
import os
from datetime import datetime

LOG_FILE=f"{datetime.now().strftime('%m_%d_%Y_%H_%M_%S')}.log"
logs_path=os.path.join(os.getcwd(),"logs",LOG_FILE)
os.makedirs(logs_path,exist_ok=True)

LOG_FILE_PATH=os.path.join(logs_path,LOG_FILE)

logging.basicConfig(
    filename=LOG_FILE_PATH,
    format="[ %(asctime)s ] %(lineno)d %(name)s - %(levelname)s - %(message)s",
    level=logging.INFO,


)

add code in data_ingestion
add code in data_transformation
add code in utils
add code in model_traineer
