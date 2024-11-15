# Setting Up ELK Stack on Kali Linux: Elasticsearch, Logstash, Kibana

This repository provides detailed step-by-step instructions on how to install and configure the ELK Stack (Elasticsearch, Logstash, Kibana) on a Kali Linux machine. The ELK Stack is a powerful toolset used for centralized logging, monitoring, and visualizing data in real-time, which is widely adopted in cybersecurity and networking.

## Prerequisites

- **Kali Linux**: A machine running Kali Linux. Ensure your package lists are up-to-date.
- **Sufficient Disk Space**: Elasticsearch and Logstash may require significant storage space.
- **Administrative Privileges**: You will need root privileges to install packages.
- **Internet Connection**: To download and install the necessary packages.

## Steps to Install ELK Stack

### 1. Update System Packages

First, ensure all the existing packages are up to date:
```bash
sudo apt update && sudo apt upgrade -y
```

### 2. Install Java

Elasticsearch requires Java to run. Install the Java package with the following command:
```bash
sudo apt install openjdk-11-jdk -y
```
Verify that Java is installed:
```bash
java -version
```

### 3. Install Elasticsearch

To install Elasticsearch, follow these steps:

1. **Add Elasticsearch GPG Key**
   ```bash
   wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
   ```

2. **Add Elasticsearch Repository**
   ```bash
   echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list
   ```

3. **Install Elasticsearch**
   ```bash
   sudo apt update
   sudo apt install elasticsearch -y
   ```

4. **Enable and Start Elasticsearch**
   ```bash
   sudo systemctl enable elasticsearch
   sudo systemctl start elasticsearch
   ```

5. **Verify Elasticsearch Installation**
   Use the following command to verify that Elasticsearch is running:
   ```bash
   curl -X GET "localhost:9200/"
   ```
   You should see a JSON response with cluster details.

### 4. Install Logstash

Logstash is used to process and transform the data before it is indexed in Elasticsearch.

1. **Install Logstash**
   ```bash
   sudo apt install logstash -y
   ```

2. **Enable and Start Logstash**
   ```bash
   sudo systemctl enable logstash
   sudo systemctl start logstash
   ```

### 5. Install Kibana

Kibana provides a web interface for searching and visualizing logs from Elasticsearch.

1. **Install Kibana**
   ```bash
   sudo apt install kibana -y
   ```

2. **Enable and Start Kibana**
   ```bash
   sudo systemctl enable kibana
   sudo systemctl start kibana
   ```

3. **Configure Kibana**
   Edit the Kibana configuration file to allow remote access:
   ```bash
   sudo nano /etc/kibana/kibana.yml
   ```
   Uncomment and modify the following line to allow external access (replace with your machine's IP address):
   ```
   server.host: "0.0.0.0"
   ```

### 6. Configure Firewall Rules

Open the necessary ports for Kibana and Elasticsearch:
```bash
sudo ufw allow 5601/tcp
sudo ufw allow 9200/tcp
```

### 7. Access Kibana

After starting the Kibana service, you can access it through your web browser:
- Open a browser and go to: `http://<your-ip-address>:5601/`

### Troubleshooting

- If Elasticsearch fails to start, check the logs for errors:
  ```bash
  sudo journalctl -xeu elasticsearch.service
  ```
- Common errors are related to memory settings or configuration issues in the `elasticsearch.yml` file.

## Summary

In this guide, you learned how to set up the ELK stack on a Kali Linux system. The stack enables powerful logging, analysis, and visualization capabilities, which are valuable for monitoring and securing systems in real-time. This setup will serve as a foundation for data analytics, security monitoring, and incident response.

Feel free to explore more advanced configurations, such as adding data shippers like **Filebeat** or using **Logstash pipelines** for data enrichment. Contributions and suggestions are always welcome!

### [Repository Link](#) (Link to be updated once the repository is created)

