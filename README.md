# Selenikit

Selenikit gives you 2 rake tasks to run your rspec tests with Selenium or Capybara-Webkit.  It also sets up your Selenium and Capybara-Webkit drivers, links them to the Rspec tests, and looks for your test server on localhost:80.  This was designed to work on Ubuntu 12.04.

## Installation

Add this line to your application's Gemfile:

    gem 'selenikit', git: "https://github.com/cloudspace/selenikit.git"

And then execute:

    $ bundle

## Packages

You will need to install the following packages

    $ sudo apt-get install java-common firefox xvfb xorg xserver-xorg xinetd vnc4server libvncserver0 libicu48
    
Make sure you start vnc4server and set a password for it. Remember this password for VNC connections later to see what your tests are doing! Be sure to kill the VNC process using the vnc4server command:

    $ vnc4server :1
    Set password when prompted
    Verify password when prompted
    $ vnc4server -kill :1

## Setup

You will need to add 2 lines to spec_helper.rb

At the top with all of your requires add:
    
    require 'selenikit/rspec'
        
Inside the Rspec.configure block add:
    
    Selenikit::Rspec::Configure.set_driver
    
All of your integration tests should be inside of spec/features:

    Selenikit will recognise any .rb files inside of spec/features 
    as well as any .rb files in any subdirectory of spec/features
        
## Usage

Make sure you have a test server running on port 80

    $ sudo rails s -p 80 -e test

To run your tests with Selenium because you'd like a GUI

    rake spec:selenium

To run your tests with Capybara-Webkit because you want them to be fast

    rake spec:webkit