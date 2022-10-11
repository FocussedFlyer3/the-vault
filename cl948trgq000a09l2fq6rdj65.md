# How to setup custom domain SSL on Google Cloud Storage

Google Cloud Storage (GCS) is a great place to host your website’s assets, including images, video, and more. Besides, if you ever need a quick way to host a simple static website, GCS is the way to go as it is faster, cheaper, and easy to maintain.

By default upon accessing any of the buckets in your GCS with Google’s domain `(storage.googleapis.com/<bucket-name>)`, it is SSL enabled. But when you want to access the bucket with your custom domain, GCS doesn’t enable SSL for you. Thus, we need to get creative to configure SSL on our custom domain.

There are 2 ways to go around this problem. One is using **Google Load Balance**, which allows us to terminate SSL handshake on any incoming traffic. But one caveat with this is **Google Load Balancer** starts at about $18/month 😰 Damn, I am not about to spend 18 bucks every month just so I can run an HTTPS custom domain on my website’s asset. Clearly, there must be a better way to do this.

The second option is by routing all traffic with **Cloudflare**. There are many advantages to using **Cloudflare**, including performance boost, better security, and more. (I swear this is not sponsored — just want to share how awesome **Cloudflare** is and I personally love it). By default, all traffic through **Cloudflare** is secured with the free SSL. And guess what, all these are included in their free tier 🥳

Now, the how?

1. First head over [Cloudflare](https://www.cloudflare.com/) and create an account.
2. Add in your website domain and click “Add site”.
![e6492707-setting-up-cloudflare-with-your-domain-1024x545.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1642836770449/H4Cl1dhvY.png)

3. Select the free tier plan at the bottom and click “Continue”
4. It should start scanning DNS records available on your domain. Once done, click “Continue”
5. Change the name server of your domain to Cloudflare at your domain registrar. By changing the name server, you will route all traffics to go through Cloudflare’s network instead. Once done, click “Done, check nameservers”
![8f3a814b-change-domain-name-servers-1024x861.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1642836812198/p2otWSlIt.png)

6. This might take some time before the DNS gets updated. But once it is done, you should be able to see your site status becomes active at the dashboard.  

Voila! You have fully transferred your site to utilize Cloudflare’s network. Now the part to point your custom domain to GCS bucket.

7. Now in Cloudflare dashboard, click into your site and select DNS tab.
![215c4296-cloudflare-dashboard-dns-1024x148.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1642837004524/P2My5M_4j.png)

8. Click “Add record” and add a CNAME type record where you want to serve your GCS content. Once added, it might take some time before the DNS gets updated. So give it a few minutes. Once ready, you should be able to access the GCS bucket. The below example is serving GCS content with a sub-domain. So accessing image.thevaultpress.com will serve GCS bucket content. 
![eba65134-serving-gcs-content-with-subdomain-1024x313.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1642837047946/uORa-cFV8.png)

You might realize that the connection is not secure and the browser might throw an error page stating there is an SSL certification mismatch. There is still a little more tweaking needed.

> While you can serve your content through HTTPS using direct URI’s such as https://storage.googleapis.com/my-bucket/my-object, when hosting a static website using a CNAME redirect, Cloud Storage only supports HTTP. To serve your content through a custom domain over SSL, set up a load balancer, use a third-party Content Delivery Network with Cloud Storage, or serve your static website content from Firebase Hosting instead of Cloud Storage.

Apparently, DNS redirect feature on c.storage.googleapis.com does not work for HTTPS addresses, it is a HTTP-only traffic. We might need a specific settings to specifically handle this.

9. Select the Rules tab at the top (Cloudflare dashboard).

10. Click “Create Page Rule”

11. Enter the url that you be pointing to GCS. In this example, I be pointing image.thevaultpress.com to GCS.

12. Under settings search for and select “SSL”

13. Under SSL settings, select “Flexible”.  
It should look something like this after following the above configurations
![ebde7bb2-cloudflare-create-page-rule-1024x471.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1642837155778/TxdAH1hIq.png)

14. If all looks good, then click “Save and Deploy”. Do give it a few minutes for the SSL settings to be applied.

BOOM  🙌 

Now your connection is secured and no error is being thrown by the browser. No doubt this requires slightly more steps to configure, but if you want to save some bucks every month, this is the way!