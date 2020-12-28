# terraform-kitchen-aws
Example of terraform test with kitchen

## Pre-requirements
- [git](https://git-scm.com/downloads) need to be installed 
- [terraform](https://www.terraform.io/downloads.html) need to be installed 
- [kitchen-terraform](https://github.com/newcontext-oss/kitchen-terraform)
- [rbenv](https://github.com/rbenv/rbenv)
- [aws account](https://aws.amazon.com/free/)

## How to consume

```bash
git clone git@github.com:base-line/terraform-kitchen-aws.git
cd terraform-kitchen-aws
```

for simplicity I use Vagrant box with all dependencies installed. you can choose to install all this to local machine.

```bash
vagrant up
vagrant ssh
```

this example is using ruby version `2.7.1` you might edit  `Gemfile` with different version and execute the next steps accordingly

will be using [rbenv](https://github.com/rbenv/rbenv) to install required environment

```bash
curl -sL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-installer | bash -
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
source ~/.bashrc
rbenv install 2.7.1
rbenv global 2.7.1
ruby -v
gem install -r bundler
cd /vagrant
bundle install
```

## AWS credentials
don't forget AWS credentials. 

```bash
export AWS_ACCESS_KEY_ID=<ACCESS-KEY>
export AWS_SECRET_ACCESS_KEY=<SECRET-KEY>
```              

## Adjust the environment

make sure you have correct values in `testing.tfvars`

```bash
key_name = "sharply-tidy-malamute"
region = "eu-central-1"
ami = "ami-0502e817a62226e03"
instance_type = "t2.micro"
```



## Testing
as soon as environment is ready, create testing instance

converge and verify

```bash
bundle exec kitchen converge
bundle exec kitchen verify
```

the output should be similar to this

```bash
Command: `lsb_release -a`
  stdout
    is expected to match /Ubuntu/

Finished in 0.07559 seconds (files took 1.02 seconds to load)
1 example, 0 failures

$$$$$$ Finished verifying the 'default' system.
$$$$$$ Finished verifying the systems.
       Finished verifying <default-ubuntu> (0m1.06s).
-----> Test Kitchen is finished. (0m1.50s)
```

destroy the environment

```bash
bundle exec kitchen destroy
```
