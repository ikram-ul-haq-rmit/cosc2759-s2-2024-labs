# RUN AWS Academy git clone https://github.com/rmit-sdo-2024-s2/cosc2759-sem1-2024-labs

cd lab08 echo "" > ~/.aws/credenxxxxx vim ~/.aws/credenxxxxx #make sure credentials are working aws s3 ls curl ifconfig.co #131.170.239.16 vim infra/you.auto.tfvars #Updte IP #Replace lab09 references to lab08 in deploy-fixtures.sh chmod +x deploy-fixtures.sh ./deploy-fixtures.sh #appbox_public_hostname = "ec2-107-23-221-105.compute-1.amazonaws.com" #logbox_public_hostname = "ec2-54-198-25-168.compute-1.amazonaws.com" #See appbox_public_hostname value curl http://ec2-107-23-221-105.compute-1.amazonaws.com

# Check below url on Browser http://ec2-54-198-25-168.compute-1.amazonaws.com:5601/status http://ec2-54-198-25-168.compute-1.amazonaws.com:5601/app/logs/stream

ssh ubuntu@"$(terraform output -raw appbox_public_hostname)" -i infra/my_lab08_key #fixed #if not working then use direct dns ssh ubuntu@ec2-107-23-221-105.compute-1.amazonaws.com -i infra/my_lab08_key

tail /var/log/nginx/access.log

tail -f /var/log/nginx/access.log #Note in another window access nginx server you will see outputs in above curl http://ec2-54-87-167-196.compute-1.amazonaws.com/

# Set up Filebeat ssh ubuntu@"$(terraform output -raw appbox_public_hostname)" -i infra/my_lab08_key

Use carefully
curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elastic.gpg

echo "deb [signed-by=/usr/share/keyrings/elastic.gpg] https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list

sudo apt update sudo apt install filebeat

# Copy contents of "misc/filebeat.yml" and replace with "/etc/filebeat/filebeat.yml" #Replace IP Address/DNS of logbox sudo nano /etc/filebeat/filebeat.yml

sudo systemctl restart filebeat
