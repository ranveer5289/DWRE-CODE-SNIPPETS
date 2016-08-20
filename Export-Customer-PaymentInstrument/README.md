Follow the instructions present in below **KB article** on how to create a RSA key-pair to encrypt/decrypt the creditCard number of the customer's saved PI

**NOTE : I created certificate with all the fields empty and also my p12 key didn't had any password**

support-demandware.force.com/customer/kA2a0000000PIVA

You will observe that even after using RSA key-pair when you try to decrypt the CC number it returns masked CC only.

Relevant discussion on xchange : https://xchange.demandware.com/thread/19236

**Due to data retention security policy DWRE permanently masks the CC number.**

I wanted to check if the steps mention in KB article work or not. So, in order to validate that, I changed the data retention policy of site on my local sandbox.

In order to change that go to `Merchant Tools >  Site Preferences >  Order` and look for `Payment Information Retention`

![Order Preferences](/images/BM.png)

Enter an arbitrary value in it like `2`

So, by changing this value you are stating that DWRE should not mask any payment related information for 2 days and after that it will automatically mask that information.

After making the change for your specific site, go to your storefront and do the following:

* login
* Go to my-account
* Add a new payment method
* In BM configure a JOB to run the code(pipeline Export-CustomerPI)

After running the JOB you should be able to see unmasked CC in `decCC` variable.
