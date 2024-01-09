
# Lab 5: Terraform Basics

Retrieve the `terraform` binary by downloading a pre-compiled binary or compiling it from source.


To install Terraform, find the [appropriate
package](https://developer.hashicorp.com/terraform/install) for your system
and download it as a zip archive.

After downloading Terraform, unzip the package. Terraform runs as a
single binary named `terraform`. Any other
files in the package can be safely removed and Terraform will still
function.


```
cd ~/Desktop/

wget https://releases.hashicorp.com/terraform/1.6.6/terraform_1.6.6_linux_amd64.zip

unzip terraform_1.6.6_linux_amd64.zip
```


Finally, make sure that the
`terraform` binary is
available on your `PATH`. This process
will differ depending on your operating system.



Print a colon-separated list of locations in your
`PATH`.


```
$ echo $PATH
```




Move the Terraform binary to one of the listed locations. This command
assumes that the binary is currently in your downloads folder and that
your `PATH` includes
`/usr/local/bin`, but you can
customize it if your locations are different.


```
$ mv ~/Desktop/terraform /usr/local/bin/
```


### Verify the installation


Verify that the installation worked by opening a new terminal session
and listing Terraform\'s available subcommands.


```
$ terraform -help
Usage: terraform [-version] [-help] <command> [args]

The available commands for execution are listed below.
The most common, useful commands are shown first, followed by
less common or more advanced commands. If you're just getting
started with Terraform, stick with the common commands. For the
other commands, please read the help and docs before usage.
...
```



Add any subcommand to
`terraform -help` to learn more
about what it does and available options.


```
$ terraform -help plan
```



### Troubleshoot

If you get an error that `terraform` could not be
found, your `PATH` environment
variable was not set up properly. Please go back and ensure that your
`PATH` variable
contains the directory where Terraform was installed.
