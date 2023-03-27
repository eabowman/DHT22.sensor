# DHT22.sensor
This is the script to run a DHT22 temperature and humidity sensor with a Raspberry Pi. This includes uploading the data into a csv file and automatically running the script as soon as the RaspberryPi boots up which will allow you to change power sources without having to restart the program.

Here, I am assuming that you have already attached the DHT22 to a Raspberry Pi sensor. See this [link] (https://pimylifeup.com/raspberry-pi-humidity-sensor-dht22/) for a good tutorial on setting up the sensor. Also, the initial setup is from this tutorial, and the 'humidity_logger.py' script is a modified version of the script created by Emmet.

# Install programs
1. Ensure that the latest updates have been installed on Raspberry Pi.
   
   sudo apt-get update
   sudo apt-get upgrade
   
2. Install python3 and pip.
   
   sudo apt-get install python3-dev python3-pip
   
3. Check that the latest versions of the setuptools, wheel, and pip python packages have been installed.
   
   sudo python3 -m pip install --upgrade pip setuptools wheel
   
4. Using pip, install Adafruit's DHT library to the Raspberry Pi. We will need this to interact with the DHT22 sensor.

   sudo pip3 install --install-option="--force-pi" Adagruit_DHT

# Have the sensor upload data to csv file
For this, you will need to know a) the GPIO pin your sensor is attached to, b) the file path to your csv file, and c) how often you want the data logged (e.g., every second, every hour...). These will need to be altered in the 'humidity_logger.py' file. There are comments marking where these will need to be changed.

# Set up 'humidity_logger.py' script to run automatically
1. Create a systemd service file: Create a file names 'humidity_logger.service' in the '/etc/systemd/system/' directory. You will likely need to use 'sudo' to have the necessary permissions. In this file, you should define the details of your service, including the name, description, and the command that runs the script. See the 'humidity-logger.service' file. 
   Be sure that the file path to the 'humidity_logger.py' file is correct.

2. Enable the service: Once the service file is created, enable it by running the following command in a terminal. This will make the service start automatically at boot time.

    sudo systemctl enable humidity_logger.service

3. Start the service: Start the service manually by running the following command
    '''    
    sudo systemctl start humidity_logger.service
    '''
  This will start you 'humidity_logger.py' script and begin loggin data to the CSV file.

To check the status of the service

    sudo systemctl status humdity_logger.service
    
To stop the 'humidity_logger' service use

    sudo systemctl stop humidity_logger.serice
