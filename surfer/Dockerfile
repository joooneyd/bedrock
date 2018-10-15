# Use an official Python runtime as a parent image
#FROM centos:7
FROM junaidskhan/bedrock-surfer:0.2

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

RUN yum -y install unzip

RUN yum -y install epel-release && yum clean all
RUN yum -y install python-pip && yum clean all
RUN pip install --upgrade pip

RUN curl -O https://releases.hashicorp.com/terraform/0.11.8/terraform_0.11.8_linux_amd64.zip
RUN unzip terraform_0.11.8_linux_amd64.zip -d /usr/bin/
RUN echo $"export PATH=\$PATH:$(pwd)" >> ~/.bash_profile
RUN source ~/.bash_profile
RUN terraform -v

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 8080

# Define environment variable
ENV NAME Dev

# Run app.py when the container launches
CMD ["python", "app.py"]