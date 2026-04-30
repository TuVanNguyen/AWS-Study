# SES: Simple Email Service

* Scalable, highly available email
    * for marketers and app devs sending emails to customers (similar to mailchimp)
    * pay-as-you-go model
    * can also receive emails, which go to S3 bucket
    * can trigger Lambda and SNS notifications

### Applications
* automated emails e.g transaction confirmations, updates, campaigns

### Compared to SNS
* SES is email only, whereas SNS does other formats in addition to email (SMS, HTTP,SQS )
* SNS is subscription based, so consumers need to be subscribed to topic to receive messages; whereas SES just requires recepient email addresses
* SNS can't receive messages, it just publishes to a topic
