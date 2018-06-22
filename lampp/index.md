# LAMPP Stack

I love LAMPP stack. Here are a few quickthroughs on how to do it.

## Setting up Virtual Hosts

It's sexier to develop on a sexy web address, like `mydevproject.local` 
instead of the default `localhost/mydevproject`. For the purpose of this 
guide, the project is named `mydevproject`

1. Open up apache `httpd.conf`

        sudo gedit /opt/lampp/apache2/conf/httpd.conf
        
2. Enter something like this

        <VirtualHost *:80>
            ServerAdmin webmaster@dummy-host.example.com
            DocumentRoot "/opt/lampp/htdocs/mydevproject"
            ServerName mydevproject.local
            ServerAlias www.mydevproject.local
            ErrorLog "logs/mydevproject.local-error_log"
            CustomLog "logs/mydevproject.local-access_log" common
        </VirtualHost>
        
    The server is now ready to handle a custom virtual host
    
3. Set up your machine's hosts file to route your custom domain to your localhost server:

	Open up `/etc/hosts` file
    
        sudo gedit /etc/hosts
        
4. Append this line

        127.0.0.1   mydevproject.local www.mydevproject.local
        
5. Restart lampp

        sudo /opt/lampp/lampp restart
        
Now you should be able to reach your local project by typing 
in `http://mydevproject.local` into your browser

