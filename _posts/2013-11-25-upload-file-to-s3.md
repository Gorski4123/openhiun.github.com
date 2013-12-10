---
layout: post
title:  "Upload file to S3"
date:   2013-11-25 15:46:10
categories: e
permalink: /upload-file-to-s3
image: http://farm8.staticflickr.com/7427/11310438965_f80fedd890_o.jpg
---

Amazon Web Services(aka AWS) Simple Storage Service(aka S3) is static file storage in the cloud.
Developing php web application, storing photo like profile and feeds photo is essential of service.

Let's check the code!
First, you need to download AWS SDK for PHP to access AWS services. SDK helps to access, create, update and delete 
all of aws service with programmatically. In this case we are using php.

##Installing SDK
Install in PHP is simple. PHP is script, interpretable language. So just download bunch of PHP file(It's SDK!) 
and unzip it with following commends. Make sure SDK will included in your PHP file. So download SDK in same directory to
your PHP application is runnig.

{% highlight php %}
$ wget https://github.com/aws/aws-sdk-php/archive/master.zip
$ unzip master.zip
{% endhighlight %}

BTW if you troubling with unzipping zip file, Install unzip with ``sudo yum install unzip`` or ``sudo apt-get install unzip`` commend.

##Coding
Ok. now SDK are installed and let's check the code from above.

{% highlight php %}
<?php//..
//load aws sdk loader 
require './aws-sdk-php-master/build/aws-autoloader.php';
 
use Aws\Common\Aws;
use Aws\S3\Enum\CannedAcl;
//..?>
{% endhighlight %}

Load autoloader and use some of AWS SDK. and now define secret and access key and bucket you created.

{% highlight php %}
<?php//..
//define keys and bucket
$accesskey = 'access_key';
$secretkey = 'secret_key';
$bucket = 'springvil';
//..?>
{% endhighlight %}

Now this is th main part. Insert your authentication information to variable ``$s3`` and execute ``putObject`` 
class with with ``$s3`` variable. Simple is that. 

{% highlight php %}
<?php//..
try{
    // Instantiate an S3 client
    $s3 = Aws::factory(array(
        'key'=>$accesskey,
        'secret'=>$secretkey
    ))->get('s3');
    // Upload a publicly accessible file. File size, file type, and md5 hash are automatically calculated by the SDK
    $result = $s3->putObject(array(
        'Bucket' => $bucket,
        'Key'    => $profile_picture_name,
        'Body'   => $uploadfile,
        'ACL'    => CannedAcl::PUBLIC_READ,
        'ContentType'=>mime_content_type($uploadfile)
    ));

    $list = $s3->listObjects(array(
        'Bucket' => $springvil
    ));
} catch(S3Exception $e){
    print_r($e);
}
{% endhighlight %}

*Header Picture by <a href="http://www.flickr.com/photos/lwr/2368783493">Flickr</a> with <a href="http://creativecommons.org/licenses/by-nc-sa/2.0/">CC BY-NC-SA 2.0 License</a>*
