# laraApp
Vivid and working instructions on how to deploy a larval app to a subdomain when using a shared host

# First
Create your subdomain with its root pointing to a folder under your public_html
E.g:  http://app.example.com
root: /home/public_html/app/

# Second
Create a folder within the new subdomain
E.g:  http://app.example.com/realsite
root: /home/public_html/app/realsite

# Third
Upload you laravel website (zip up everything within the laravel web app and upload) to the realsite folder
