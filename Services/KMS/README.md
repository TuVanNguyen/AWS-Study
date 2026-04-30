# KMS (Key Management Service)
* use to create and control encryption keys
* integrates with other services to encrypt data with the keys e.g S3, RDS

### Why Use
* you're storing sensitive data that you want to keep secret
    * e.g customer data, passwords, secrets, credentials

### Features
* key rotation: you can set AWS to rotate keys automatically every 365 days
* multi-tenant: a single instance of the service serves multiple customers (the tenants)

### Limitations
* KMS encryption keys are single region by default
* KMS encryption keys can not be exported out of KMS in plaintext

### Integrates with (most common, not exhaustive)
* S3
* RDS
* DynamoDB
* Lambda
* EBS
* EFS
* CloudTrail
* Developer Tools

## CMK (Customer Master Key)
* encrypts/decrypts data up to 4 KB
* implements envelope encryption
    * CMK generates, encrypt, and decrypt data key
    * the data key encrypts and decrypts data

### Attributes
* alias
* creation date
* description
* key state: enabled/disabled/pending deletion/unavailable
* key material: to generate key, can be provided by you or AWS


## Important API calls
* **aws kms encrypt**: encrypts plaintext to ciphertext using CMK
* **aws kms decrypt**: decrypts ciphertext to plaintext using CMK
* **aws kms re-encrypt**: decrypts ciphertexts then re-encrypts it with different key e.g when CMK is rotated
* **aws kms enable-key-rotation**: automatic key rotation every 365 days
* **aws kms generate-data-key**: create data-key using CMK








