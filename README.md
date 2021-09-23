# SRE_Grafana


# SRE AWS instance with CloudWatch linked to Grafana
 
## Set-up
1. Create a new `Ubuntu 18.04` EC2 instance in `eu-west-1`
2. In order to connect Grafana to AWS the aws access and secret keys are required
3. Grafana runs on `port 3000` so we need a security group that allows access along with `80` and `22`
4. Secure shell into your created EC2 instance
 
--------------------------------

## Installation of Grafana
1. Run `sudo apt-get update -y` followed by `sudo apt-get upgrade -y` incase any missing packages
2. `sudo apt-get -y adduser libfontconfig1`
3. `wget https://dl.grafana.com/enterprise/release/grafana-enterprise_8.1.5_amd64.deb`
4. `sudo dpkg -i grafana-enterprise_8.1.5_amd64.deb`
5. `sudo nano /etc/apt/sources.list`
6. add this to the end of the nano file `deb https://packagecloud.io/grafana/stable/debian/ stretch main` and save
7. Back to the terminal use `curl https://packagecloud.io/gpg.key | sudo apt-key add -`
8. `sudo systemctl daemon-reload`
9. `sudo systemctl start grafana-server`
10. `sudo systemctl status grafana-server`
11. `sudo systemctl enable grafana-server.service`
12. `sudo service grafana-server start`
13. `sudo nano /usr/share/grafana/.credentials`

Use this structure in the file and add your aws keys:

    [default]
    aws_access_key_id = *********************
    aws_secret_key_id = ********************
    region = eu-west-1

15. `sudo chmod 0644 /usr/share/grafana/.credentials`

