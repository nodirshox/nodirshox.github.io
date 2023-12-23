---
layout: post
title: "Load testing in 5 minutes"
categories: ["tutorial", "programming", "testing"]
permalink: /load-testing-in-5-minutes
---

Handling massive loads is plays a crucial role in web development. It is good practice to test your API s for getting an overall image on huge traffic. There are plenty of awesome tools for testing purpose.

One of the famous tool is called [JMeter](https://jmeter.apache.org/){:target="_blank"}. This application developed by Apache and an open source project. You can make load tests for:

- HTTP, HTTPS
- FTP
- SMTP
- ...

The core of JMeter is Java language. So we need to have a Java environment on your local/remote machine. Let's get started from scratch on Ubuntu OS.

# Step 1 - Setting Java

First check your system whether you have a Java or not:

```
java --version
```

Latest version of JMeter requires Jave 8+ version.


If you see something like this, you are good to go move on next step:

![Screenshot](/assets/2021-01-31-load-testing/testing-1.jpg)

If your result "The program ''java' can be found ..." you can install Java by following([full tutorial](https://linuxhint.com/install-java-9-on-ubuntu/){:target="_blank"} for installing Java):

```
sudo apt install openjdk-9-jre
```

# Step 2 - Download JMeter

You need download binary of program from JMeter official website:

[https://jmeter.apache.org/download_jmeter.cgi](https://jmeter.apache.org/download_jmeter.cgi){:target="_blank"}

Let's download in terminal (~70 MB):

```
wget https://downloads.apache.org//jmeter/binaries/apache-jmeter-5.4.1.tgz
```

Next unzip an archive:

```
tar xf apache-jmeter-5.4.1.tgz
```

Next change directory to apache/bin folder:

```
cd apache-jmeter-5.4.1/bin
```

Launch GUI application

```
./apache
```

# Step 3 - Write test plan

Firstly we need a create test file. So previous step you launched GUI of JMeter and we will do some configuration. It is good to do this on your computer, not a remote server. After finishing configuration you can test it on powerful remote server.

Give a name to your test(default: Test Plan):

![Screenshot](/assets/2021-01-31-load-testing/testing-2.jpg)

Then right click on left side to your "Project name"

![Screenshot](/assets/2021-01-31-load-testing/testing-3.jpg)

And there are 3 parts:

**Number of Threads (users)** - number of visitors/requests to your website

**Ramp-Up Period (in seconds)** - delay period between 2 theads.

**Loop count** - number of loops for threats. You can make it infinite by selecting checkbox.

![Screenshot](/assets/2021-01-31-load-testing/testing-4.jpg)

Next we will test our API by adding HTTP request:

![Screenshot](/assets/2021-01-31-load-testing/testing-5.jpg)

I want to test just the GET method for tutorial purpose. You can make any type of HTTP request (GET, POST, Patch, ...).

![Screenshot](/assets/2021-01-31-load-testing/testing-6.jpg)

This is end of preparing part. We need to save this plan in ".jmx" format by clicking save button.

# Step 4 - Run a test

There are 2 types of to run a test file.

1. On GUI - this method is not perfect massive loads such as 10~50K~... . But by doing a test on GUI, we will make sure everything is correct on test plan.

Let's get summery result. You can choose any type of report.

![Screenshot](/assets/2021-01-31-load-testing/testing-7.jpg)

Now you can click green "Play" button top sidebar.

2. On terminal - you can get a powerful remote server(and good Internet connection) and do massive tests on this method. If it is a new server, you need to repeat 1, 2 steps on a server to configuration.
Next, we need create .jmx file and copy all codes saved from step 3.

Open server's terminal and go to JMeter's folder and create a new by following:

```
touch test.jmx
```

Copy all codes from your local code and paste it to this file, save it:

```
nano test.jmx
```

# Running test file on terminal

Make sure your on folder on ./bin folder

```
pwd
```

Run script:

```
./jmeter -n -t test.jmx
```

Result

![Screenshot](/assets/2021-01-31-load-testing/testing-8.jpg)

By default JMeter is allocates only 1 GB RAM, if you want to increase and allocate more size, open jmeter in Text editor, change this lines:

```
"${HEAP:="-Xms1g -Xmx1g -XX:MaxMetaspaceSize=256m"}"
```

If you want increase 1 GB to 8GB change to this and save the file:

```
"${HEAP:="-Xms8g -Xmx8g -XX:MaxMetaspaceSize=256m"}"
```


If you want to save logs as file add -l flag and filename to option:

```
./jmeter -n -t test.jmx -l logs.txt
```

# Conclusion

Now you are learned how make load tests. Feel free contact to me any question and suggestions mr.nodirbek77@gmail.com

[Link](https://ergashevn.blogspot.com/2021/01/load-testing-in-5-minutes.html){:target="_blank"}
