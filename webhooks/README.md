# Webhooks Receiver

Plate Recognizer lets you forward the inference results to a third party. Here are examples for how to use our [webhook API](http://docs.platerecognizer.com/#webhooks).

- [Webhooks Receiver](#webhooks-receiver)
  - [Sample Code](#sample-code)
    - [Python Without Dependencies](#python-without-dependencies)
    - [Python and Flask](#python-and-flask)
    - [Javascript / Node](#javascript--node)
    - [C# / .Net Framework v4.8:](#c--net-framework-v48)
  - [Sending Data to the Webhook Receiver](#sending-data-to-the-webhook-receiver)
  - [Home Assistant](#home-assistant)
  - [Webhook via AWS Lambda](#webhook-via-aws-lambda)
  - [Webhook Middleware](#webhook-middleware)

## Sample Code

After starting the receiver, configure Snapshot or Stream webhooks in Plate Recognizer with the URL http://<your-machine-ip>:8001/.

### Python Without Dependencies

```shell
python3 webhook_reader.py
```

### Python and Flask

```shell
pip install Flask==1.1.2
python3 webhook_reader_flask.py
```

### Javascript / Node

```shell
npm install
node webhook_reader.js
```

### C# / .Net Framework v4.8:

Install [this NuGet package](https://github.com/Http-Multipart-Data-Parser/Http-Multipart-Data-Parser) required for MultiPart Parsing

```shell
Install-Package HttpMultipartParser
```

Build Solution and Run WebhookReader.exe as a Console Application

## Sending Data to the Webhook Receiver

1. Find your machine local IP for example 192.168.0.206. You can use `ifconfig` to get it.
2. Send an example webhook to the server. If it is running correctly, it should exit without an error.
3. Optionally, you can send an authentication token with `-e TOKEN=XXX` or a camera with `-e CAMERA=XXX` to identify the webhook source.

```shell
docker run -e URL=http://MY_IP_ADDRESS:8001 platerecognizer/webhook-tester
```

3. Configure the webhook on Platerecognizer.
   - In Stream, edit your `config.ini`, add the following to a camera: `webhook_target = http://MY_IP_ADDRESS:8001/`
   - For Snapshot, open [Webhooks Configuration](https://app.platerecognizer.com/service/snapshot-cloud/webhooks/).

## Home Assistant

[This project](https://github.com/adamjernst/plate-handler) uses Stream webhooks to send license plate data to a home automation server. Form there, it will send a notification.

## Webhook via AWS Lambda
[This guide](webhook_lambda/) aims to provide you with a minimum sample to receive webhook data from Snapshot/Stream on your AWS Lambda instance.

## Webhook Middleware
[This guide](https://guides.platerecognizer.com/docs/stream/integrations) will help you integrate webhooks into your applications.