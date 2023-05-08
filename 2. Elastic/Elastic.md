## How to Set Up Elastic Stack in Ubuntu 22.04.2 LTS

To set up the Elastic Stack (formerly known as the ELK stack) in Ubuntu 22.04.2 LTS, which includes Elasticsearch, Logstash, and Kibana, you can follow the steps below:

1. Update System Packages:
sudo apt update
sudo apt upgrade

2. Install Java:
Elasticsearch requires Java to run. Install OpenJDK with the following command:
sudo apt install openjdk-11-jdk


3. Install Elasticsearch:
- Download and install the Elasticsearch public signing key:
  ```
  wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
  ```

- Add the Elasticsearch repository to your system:
  ```
  echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list
  ```

- Update the package list and install Elasticsearch:
  ```
  sudo apt update
  sudo apt install elasticsearch
  ```

- Enable and start the Elasticsearch service:
  ```
  sudo systemctl enable elasticsearch
  sudo systemctl start elasticsearch
  ```

- Verify that Elasticsearch is running:
  ```
  curl -X GET "localhost:9200"
  ```

4. Install Kibana:
- Add the Kibana repository to your system:
  ```
  echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list
  ```

- Update the package list and install Kibana:
  ```
  sudo apt update
  sudo apt install kibana
  ```

- Configure Kibana to listen on the appropriate IP address:
  Open the Kibana configuration file using a text editor:
  ```
  sudo nano /etc/kibana/kibana.yml
  ```

  Locate the `server.host` setting and replace the default value with your server's IP address or hostname. Save and close the file.

- Enable and start the Kibana service:
  ```
  sudo systemctl enable kibana
  sudo systemctl start kibana
  ```

- Verify that Kibana is running:
  Open a web browser and visit `http://localhost:5601`. You should see the Kibana interface.

5. Install Logstash:
- Add the Logstash repository to your system:
  ```
  echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list
  ```

- Update the package list and install Logstash:
  ```
  sudo apt update
  sudo apt install logstash
  ```

- Create a Logstash configuration file:
  ```
  sudo nano /etc/logstash/conf.d/myconfig.conf
  ```

  Add your Logstash configuration in this file. For example, you can create a basic configuration to read from an input source and write to Elasticsearch:
  ```
  input {
    # Your input configuration here
  }

  output {
    elasticsearch {
      hosts => ["localhost:9200"]
      index => "myindex"
    }
  }
  ```

  Save and close the file.

- Test your Logstash configuration:
  ```
  sudo -u logstash /usr/share/logstash/bin/logstash -t -f /etc/logstash/conf.d/myconfig.conf
 
