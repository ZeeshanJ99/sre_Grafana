# What is Grafana

- Grafana is an open source solution for running data analytics, pulling up metrics that make sense of the massive amount of data & to monitor our apps with the help of cool customizable dashboards.

- Grafana connects with every possible data source, commonly referred to as databases such as Graphite, Prometheus, Influx DB, ElasticSearch, MySQL, PostgreSQL etc.

- Grafana being an open source solution also enables us to write plugins from scratch for integration with several different data sources.

- The tool helps us study, analyse & monitor data over a period of time, technically called time series analytics. It helps us track the user behaviour, application behaviour, frequency of errors popping up in production or a pre-prod environment, type of errors popping up & the contextual scenarios by providing relative data.

----------------------------------------

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

-----------------------------------------------------------------------

## Accessing Grafana
In order to access Grafana, you need to use the Public IP of the grafana instance that we created previously with the port `IP:3000`.

You will now be shown a login page where the login details are:

- Username: `Admin` Password: `Admin`

After logging in you will be able to change the password to whatever you like.

---------------------------------------------------------------

### Adding a data source

1. On the `Welcome to Grafana page`, click the widget called `Add your first data source`.
2.  Select your chosen data source `Cloudwatch`, and the new page will look like this:

![image](https://user-images.githubusercontent.com/88186084/134772580-1c8a27a3-d950-433e-a174-d914b36ba34d.png)


3. Input your `AWS keys` in the relevant sections and add the correct region `eu-west-1`

---------------------------------------------------------

### Adding a Dashboard
On the sidebar, hover over the addition symbol and select `Dashboard`.



