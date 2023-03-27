# DHT22.sensor
This is the script to run a DHT22 temperature and humidity sensor with a Raspberry Pi. This includes uploading the data into a csv file and automatically running the script as soon as the RaspberryPi boots up which will allow you to change power sources without having to restart the program.

# Install programs

# Set up 'humidity_logger.py' script to run automatically
1. Create a systemd service file: Create a file names 'humidity_logger.service' in the '/etc/systemd/system/' directory. You will likely need to use 'sudo' to have the necessary permissions. In this file, you should define the details of your service, including the name, description, and the command that runs the script. See the 'humidity-logger.service' file. 
2. Enable the service: Once the service file is created, enable it by running the following command in a terminal. This will make the service start automatically at boot time.

    sudo systemctl enable humidity_logger.service

3. Start the service: Start the service manually by running the following command:

    sudo systemctl start humidity_logger.service

  This will start you 'humidity_logger.py' script and begin loggin data to the CSV file. 
