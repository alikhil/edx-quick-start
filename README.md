# Open EDX Fullstack. Installation and Configuration.

Here I will describe steps that I made to make edx be configured as to be used in production.

Before, make sure that your machine meet hardware requirements and that it supports nested virtualization(if you installing it on other VM). 
1. Follow [installation tutorial](http://edx.readthedocs.io/projects/edx-installing-configuring-and-running/en/latest/installation/fullstack/index.html).
2. Set AWS S3 settings. 

#### Setting AWS S3

```sh
cd fullstack
vagrant ssh
```
Update following strings in `cms.auth.json` and `lms.auth.json`

```json
{
    
    "AWS_ACCESS_KEY_ID": "your amazon s3 key id here", 
    "AWS_QUERYSTRING_AUTH": true, 
    "AWS_S3_CUSTOM_DOMAIN": null, 
    "AWS_SECRET_ACCESS_KEY": "secret key", 
    "AWS_STORAGE_BUCKET_NAME": "some bucket name", 
   
}
```

Update following strings in `cms.env.json` and `lms.env.json`

```json
    "GRADES_DOWNLOAD": {
        "BUCKET": "grades bucket", 
        "ROOT_PATH": "tmp/edx-s3/grades", 
        "STORAGE_CLASS": "django.core.files.storage.FileSystemStorage", 
        "STORAGE_KWARGS": {
            "location": "/tmp/edx-s3/grades"
        }, 
        "STORAGE_TYPE": "s3"
    }
```

[Configure other buckets](https://openedx.atlassian.net/wiki/display/OpenOPS/Use+AWS+for+Data+Storage). 

### Links

[Troubles with uploading grades to S3](https://groups.google.com/forum/#!topic/openedx-ops/uyf2kyVPyGQ)

[Steps to upload file with OpenAssessment to Amazon AWS](https://community.bitnami.com/t/steps-to-upload-file-with-openassessment-to-amazon-aws/44863)

[Configuring SMTP](https://stackoverflow.com/questions/22569426/how-can-i-config-open-edx-production-stack-smtp-settings)
