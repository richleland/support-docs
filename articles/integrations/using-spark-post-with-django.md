---
title: "Using SparkPost with Django"
redirect_from: "https://support.sparkpost.com/customer/portal/articles/2169630-using-sparkpost-with-django"
description: "Note this article covers using Spark Post via SMTP with Django We also offer a Python client library that includes a Django email backend The simplest way to use Spark Post in your Django project is to configure its SMTP backend To configure Django’s SMTP backend put the following lines..."
---

Note: this article covers using SparkPost via SMTP with Django. We also offer [a Python client library](http://python-sparkpost.readthedocs.org/) that includes a Django email backend.

The simplest way to use SparkPost in your Django project is to configure its [SMTP backend](https://docs.djangoproject.com/en/1.8/topics/email/#smtp-backend). To configure Django’s SMTP backend, put the following lines in your project’s **settings.py** file:

```
EMAIL_HOST = 'smtp.sparkpostmail.com'
EMAIL_PORT = 587
EMAIL_HOST_USER = 'SMTP_Injection'
EMAIL_HOST_PASSWORD = 'YOUR API KEY'
EMAIL_USE_TLS = True
```

Remember to replace `YOUR API KEY` with an API key that has “Send via SMTP” permission. Follow the [create API keys](https://support.sparkpost.com/customer/en/portal/articles/1933377-create-api-keys) guide for detailed instructions.

Now send your email through Django using SparkPost:

```
​from django.core.mail import send_mail

send_mail('Using SparkPost with Django', 'This is a message from Django using SparkPost!', 'django-sparkpost@sparkpostbox.com',
    ['to@example.com'], fail_silently=False)
```

Note that SMTP is the default backend for Django. However, if you want to make it explicit, put the following line in **settings.py**:

`EMAIL_BACKEND =` `'django.core.mail.backends.smtp.EmailBackend'`