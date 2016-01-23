<div markdown="1">

<h2 id="sample-clone">Install sample data by cloning repositories</h2>
This topic discusses how to get the Magento sample data if you cloned the Magento GitHub repository. This method is intended only for contributing developers (that is, developers who plan to contribute to the Magento 2 codebase).

If you're not a contributing developer, choose one of the other options displayed in the table of contents on the left side of the page.

<div class="bs-callout bs-callout-warning">
    <p>You can use sample data with either the <code>develop</code> branch (more current) or a released branch (such as <code>2.0</code> or <code>2.0.1</code> (more stable). We recommend you use a released branch because it's more stable. If you're contributing code to the Magento 2 repository and you need the most recent code, use the <code>develop</code> branch.</p>
    <p>Regardless of the branch you choose, you must <a href="{{ site.gdeurl }}install-gde/install/composer-clone.html#instgde-prereq-compose-clone">clone</a> the corresponding branch of the Magento 2 GitHub repository. For example, sample data for the <code>develop</code> branch can be used <em>only</em> with the Magento 2 <code>develop</code> branch.</p>
</div>

See the following sections:

*	<a href="#sample-prereq">Sample data prerequisites</a>
*	<a href="#clone-sample-data-deploy">Released branch&mdash;Install sample data modules</a>
*   <a href="#clone-sample-data-dev">`develop` branch&mdash;Install sample data modules</a>
*	<a href="#clone-file-perms">Set file system ownership and permissions</a>

<h2 id="sample-prereq">Sample data prerequisites</h2>
Before you install sample data, you must update Magento's `composer.json` to get components from `https://repo.magento.com`.

1.  Log in to the Magento server as, or switch to, the <a href="{{ site.gdeurl }}install-gde/prereq/apache-user.html">Magento file system owner</a>.
4.  <a href="{{ site.gdeurl }}install-gde/prereq/dev_install.html">Clone the Magento 2 GitHub repository</a>.

5.  <a href="{{ site.gdeurl }}install-gde/install/prepare-install.html">Update dependencies</a> by running `composer install`.

2.  Change to your Magento installation directory.

    For example, `/var/www/html/magento2`
3.  Require the `https://repo.magento.com` repository, which contains the sample data code:

        composer config repositories.magento composer https://repo.magento.com

4.	Optionally install the Magento software. (You can also do this after you install sample data.)

	*	<a href="{{ site.gdeurl }}install-gde/install/cli/install-cli.html">Install using the command line</a>
	*	<a href="{{ site.gdeurl }}install-gde/install/web/install-web.html">Install using the Setup Wizard</a>

4.  Continue with the next section.

<h2 id="clone-sample-data-deploy">Install sample data modules</h2>
To install sample data using the command line, enter the following command as the Magento file system owner:

    php <your Magento install dir>/bin/magento sampledata:deploy [module-list]

where `[module-list]` is an optional space-separated list of <a href="#sample-data-modules">sample data modules</a> to install. Omit this parameter to install all sample data modules.

You are required to <a href="{{ site.gdeurl }}install-gde/prereq/connect-auth.html">authenticate</a> to complete the action.

### Authentication error

The following error might display:

    [Composer\Downloader\TransportException]
    The 'https://repo.magento.com/packages.json' URL required authentication.
    You must be using the interactive console to authenticate

If the error displays, change to your Magento installation directory and run `composer update`, which will prompt you for your <a href="{{ site.gdeurl }}install-gde/prereq/connect-auth.html">authentication keys</a>.

<h3 id="sample-data-modules">Complete list of modules</h3>
The complete list of sample data modules follows:

{% include install/sampledata/sample-data_list-of-modules.md %}

## `develop` branch&mdash;Install sample data modules {#clone-sample-data-dev}
You can use this method of installing sample data *only* if all of the following are true:

*   You use Magento CE
*   You <a href="{{ site.gdeurl }}install-gde/prereq/dev_install.html">cloned the Magento 2 `develop` branch</a>.

### Clone the sample data repository {#clone-sample-repo}
This section discusses how to install Magento sample data by cloning the sample data repository. You can clone the sample data repository in any of the following ways:

*   Clone with the <a href="#instgde-prereq-sample-clone-ssh">SSH protocol</a>
*   Clone with the <a href="#instgde-prereq-compose-clone-https">HTTPS protocol</a>

#### Clone with SSH {#clone-sample-repo-ssh}
To clone the Magento sample data GitHub repository using the SSH protocol:

1.  In a web browser, go to <a href="https://github.com/magento/magento2-sample-data" target="_blank">the Magento sample data repository</a>.
2.  Next to the name of the branch, click **SSH** from the list.
3.  Click **Copy to clipboard**

    The following figure shows an example.

    <img src="{{ site.baseurl }}common/images/install_mage2_clone-ssh.png" width="650px" alt="Clone the Magento GitHub repository using SSH">
4.  Change to your web server's docroot directory.

    Typically, for Ubuntu, it's `/var/www` and for CentOS it's `/var/www/html`.

    Need <a href="{{ site.gdeurl }}install-gde/basics/basics_docroot.html">help locating the docroot?</a>
5.  Enter `git clone` and paste the value you obtained from step 1.

    An example follows:

        git clone git@github.com:magento/magento2-sample-data.git
6.  Wait for the repository to clone on your server.

    <div class="bs-callout bs-callout-info" id="info">
        <p>If the following error displays, make sure you <a href="https://help.github.com/articles/generating-ssh-keys/" target="_blank">shared your SSH key</a> with GitHub: </p>
            <pre>Cloning into 'magento2'...
Permission denied (publickey).
fatal: The remote end hung up unexpectedly</pre>
    </div>
7.  Change to the `<your Magento sample data clone dir>/dev/tools` directory.
8.  Enter the following command:
        
        php -f build-sample-data.php -- --ce-source="<your Magento CE install dir>"
9.  Wait for the command to complete.

10. See <a href="#instgde-prereq-compose-clone-perms">Set file system permissions and ownership</a>.

#### Clone with HTTPS {#instgde-prereq-compose-clone-https}
To clone the Magento sample data GitHub repository using the HTTPS protocol:

1.  In a web browser, go to <a href="https://github.com/magento/magento2-sample-data" target="_blank">the Magento sample data repository</a>.
2.  On the right side of the page, under the **clone URL** field, click **HTTPS**.
3.  Click **Copy to clipboard**.

    The following figure shows an example.
    
    <img src="{{ site.baseurl }}common/images/install_mage2_clone-https.png" width="650px" alt="Clone the Magento GitHub repository using HTTPS">
2.  Change to your web server's docroot directory.

    Typically, for Ubuntu, it's `/var/www` and for CentOS it's `/var/www/html`.
3.  Enter `git clone` and paste the value you obtained from step 1.

    An example follows:
        
        git clone https://github.com/magento/magento2-sample-data.git
4.  Wait for the repository to clone on your server.
5.  Change to the `<your Magento sample data clone dir>/dev/tools` directory.
6.  Enter the following command:

        php -f build-sample-data.php -- --ce-source="<your Magento CE install dir>"

    For example,

        php build-sample-data.php -- --ce-source="/var/www/magento2"

7.  Wait for the command to complete.
8.  See the next section.

<h2 id="clone-file-perms">Set file system ownership and permissions</h2>
Because the `php build-sample-data.php` script creates symlinks between the sample data repository and your Magento 2 repository, you must set file system permissions and ownership in the sample data repository. Failure to do so results in errors accessing the storefront.

To set file system permissions and ownership on the sample data repository:

1.  Change to your sample data clone directory.
2.  Set ownership:

        chown -R :<your web server group name> .

    Typical examples:

    CentOS: `chown -R :apache .`

    Ubuntu: `chown -R :www-data .`

3.  Set permissions:

        find . -type d -exec chmod 770 {} \; && find . -type f -exec chmod 660 {} \;
    
    If you must enter the commands as <code>sudo</code>, use:

        sudo find . -type d -exec chmod 770 {} \; && sudo find . -type f -exec chmod 660 {} \;
3.  Clear static files:

        cd <your Magento CE install dir>/var
        rm -rf cache/* page_cache/* generation/*
 
#### Next step
Install the Magento software:

*   <a href="{{ site.gdeurl }}install-gde/install/cli/install-cli.html">Command line</a>
*   <a href="{{ site.gdeurl }}install-gde/install/web/install-web.html">Setup Wizard</a>