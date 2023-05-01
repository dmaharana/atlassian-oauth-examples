# Atlassian 3-legged OAuth Example

> I'm currently looking for people to help build examples in GWT, Java, and PHP. The Ruby version
> is done and I'm currently working on the Nodejs version. Fork this then send me a pull request
> if you want to contribute. Thanks!

Atlassian's products have a built-in OAuth provider which it uses primarily to allow cross-product 
authentication/integration through the AppLinks feature. However, you can also use it as an 
authentication source for your custom applications and as an authentication source for Atlassian's 
REST APIs. Using OAuth allows you to build your apps without asking your users for their login 
credentials.

For more info about OAuth, check out <http://oauth.net> for more information. Atlassian's products 
currently support OAuth 1.0a.

## Examples

This repository contains a collection of sample code in various languages showing how to use 
Atlassian's OAuth provider. We currently only have a Ruby/Sinatra sample, but we'll be building 
this up to include other languages and frameworks.

## Required setup

There are a few things you need to do to get these examples to work. This assumes you're using
JIRA 4.4+ or Confluence 4+.

  1. Generate an RSA pub/priv key pair. Atlassian's OAuth provider uses RSA-SHA1 to sign the 
     request. For the purpose of the examples here, you can just use the rsa.pem and rsa.pub keys
     stored in the root directory. Do not use the keys provided here for your own application. 
     [Please generate your own keys](http://www.madboa.com/geek/openssl/#key-rsa) for your own 
     application.
  2. [Configure an Application Link](http://confluence.atlassian.com/display/JIRA/Configuring+Application+Links). 
     To register an OAuth consumer, you'll need to register an Application Link inside your Atlassian 
     product. Refer to the Atlassian docs on how to do this for your product.
  3. After you've created an Application Link, configure an "Incoming Authentication" with the 
     following details:
  
         Consumer key:          dpf43f3p2l4k3l03
         Consumer name:         OAuth Test
         Description:           OAuth Test Example
         Public key:            <paste the contents of rsa.pub>
         Consumer callback URL: http://<hostname where you're hosting this code>/auth


After you've configured your OAuth consumer, go to the directory for the example you want to 
test then read the README.md for additional details.

-----------------------------------------------------------------------------------
Refer [https://developer.atlassian.com/server/jira/platform/oauth/]
# Generate an RSA public/private key pair

## In terminal, run the following openssl commands. You can do this anywhere in your file system, but note that this is where the files will be created.

    - Generate a 1024-bit private key:
`openssl genrsa -out jira_privatekey.pem 1024`

    - Create an X509 certificate:
`openssl req -newkey rsa:1024 -x509 -key jira_privatekey.pem -out jira_publickey.cer -days 365`

    - Extract the private key (PKCS8 format) to the jira_privatekey.pcks8 file:
`openssl pkcs8 -topk8 -nocrypt -in jira_privatekey.pem -out jira_privatekey.pcks8`

    - Extract the public key from the certificate to the jira_publickey.pem file:
`openssl x509 -pubkey -noout -in jira_publickey.cer  > jira_publickey.pem`

