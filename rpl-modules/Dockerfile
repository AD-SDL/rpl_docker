FROM kwelbeck/base-ros2-with-empty-overlay:latest


RUN mkdir -p /root/config/temp/




## 3 ########################################
## Copy/Add drivers and other packages from repository root directory 
## into /root directory of image 
## Commented example below downloads ot2_driver from repository root then
## installs it, including python dependencies using pip3 on the 
## requirements.txt dependency list. 
## Also upgrades numpy to fix nested dependency
##
## Uncomment and replicate as needed
## Alternatively install python packages with `python3 setup.py install`

WORKDIR /root
COPY ot2_driver/ ot2_driver/
RUN pip3 install -r ot2_driver/requirements.txt \
    && pip3 install -e ot2_driver \
    && pip install numpy --upgrade 