# This is a agent intallation command

      #!/bin/bash

      # Update system
      sudo apt-get update -y

      # Install dependencies
      sudo apt-get install -y ruby-full wget

      # Download the latest CodeDeploy agent package
      cd /tmp
      wget https://aws-codedeploy-us-east-1.s3.us-east-1.amazonaws.com/latest/install

      # Make it executable
      chmod +x ./install

      # Install the agent
      sudo ./install auto

      # Enable and start service
      sudo systemctl enable codedeploy-agent
      sudo systemctl start codedeploy-agent

# Check status
sudo systemctl status codedeploy-agent

# Restarte Agent
sudo systemctl restart codedeploy-agent
sudo systemctl status codedeploy-agent

