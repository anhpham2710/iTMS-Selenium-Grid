# iTMS-Selenium-Grid
This repo has all the scripts required to fire up a Selenium GRID. Selenium GRID creates  a network of http servers where in there are two roles  
1. Hub  

2. Node  
  
Hub is the orchestrator that takes incoming payload that contains a request for a certain configuration of browser.If the grid has a node that matches the browser configuration requested in the payload, the hub establishes a session and the script commands execute on that browser from there on. If there is no match, then hub returns an error  
  

It is assumed that you have JDK installed and JAVA_HOME environment variable is set to JDK root folder.  

**Overall Folder Structure on Windows machine:**  

# How to Start GRID 

## 1. Start Hub  
Double click START_HUB.bat  
You should see something like this  

**Hub Started:**   

## 2. Start Node with Chrome 39, Firefox 35 and IE 10 instances  
Double click START_NODE_CH39_FF35_IE10_WINDOWS.bat  
Open the bat file to see the port on which it is started. You can change this. By default 5 instances  
You can change that too by modifying it however 5 is generally a good number.  
You should see something like this  

**Node Started:**  

## 3. Create nodes with new configurations  

If you have other browser versions that you would like to start a node with, simply copy an existing START_NODEXXXX.bat and modify the versions of the browsers.   

That is it ! If you already know how a selenium GRID works, the above information should suffice. Below is more detailed explanation. Oh, logs are created in SELENIUMLOGS folder  

# GRID as windows service  

If you wish to start the GRID automatically whenever windows starts, then you can make them as windows services. Look into the SeleniumGRID-WindowsService folder.  

**Tool for creating windows service**  
Install rktools.exe on your machine. This will enable us to create windows service that can execute arbitrary commands, in our case the commands to start the jvm for hub & node

**Modify the .reg files**  
Open the Seleniumhub.reg and Seleniumnode.reg files in your favorite text editor and modify them as needed. If you leave as is, they start with default configuration i.e. 10 instances of firefox, 10 instances of chrome and 2 instances of ie [of course half of those follow Selenium RC protocol and half webdriver protocol]    

**Install the services**  
Once you have completed the above two steps, double click the SeleniumServerInstall.bat and that should create two windows services viz. SeleniumHub and SeleniumNode. You can see the services in by entering "services.msc" in your run command  

## Use specific versions of WebDriver  
The folder CHROMEDRIVERS has chrome webdrivers with folder structure the same as the one where we [download](http://chromedriver.storage.googleapis.com/index.html) chromedriver.exe. For example it has 2.12 and 2.13. If a newer version arrives, create the folder and unzip the chromedriver.exe in that folder.  

**Using specific chromedriver.exe**  
If you would like the node to use a specific version of chromedriver.exe, then open the ****.bat file and edit the key CHROME_WEBDRIVER_VERSION to the value of the folder. Don't forget to stop the node before doing this. Once you start the node at this point, it will start the ndoe with the version specified in CHROME_WEBDRIVER_VERSION  

The folder IEDRIVERS has ie webdrivers with folder structure the same as the one where we [download](http://selenium-release.storage.googleapis.com/index.html) IEDriverServer.exe. For example it has 2.43 and 2.44. If a newer version arrives, create the folder and unzip the IEDriverServer.exe in that folder.  

**Using specific IEDriverServer.exe**  
If you would like the node to use a specific version of IEDriverServer.exe, then open the ****.bat file and edit the key IE_WEBDRIVER_VERSION to the value of the folder. Don't forget to stop the node before doing this. Once you start the node at this point, it will start the ndoe with the version specified in IE_WEBDRIVER_VERSION  

At this point, we have only chrome and ie drivers, but you can easily extend this model to include safari , opera and create folders and then include the variables in the .bat files  

## Use browser binaries  
We explicitly set the browser binary path in the .bat script. See the variables CHROME_BINARY_LOC & FIREFOX_BINARY_LOC. So you might have to change those based on where the browser binaries are located  

## Use Selenium version  
This helper has 2.44.0 selenium jar included, hence it uses that. If you wish to use another one, download the x.y.z.jar, place it in the root folder and modify the variable value SELENIUM_VERSION in the .bat files to use the x.y.z. You might have to change this variable value in both hub and node batch scripts  

## Using json Config  
We have two json config files for hub and node and associated batch scripts that use this config. The config files use the same options that CH39_FF35_IE10 command line batch script uses, because I had those versions of browsers on my machine. If you would like to use different versions, then you will have to edit the values inside the config files.  

## Ports  
The batch files specify 4444 port for hub and 5555,5556 and so on port numbers for nodes. You may change them if you wish to or add new ones based on port availability  

# Finally  
There is a reason why we have used the structure CH39_FF35_IE10. Its because it aligns with using the [saucelabs](https://github.com/machzqcq/saucelabs) gem, that creates a RemoteWebDriver instance with a single line of code (at the minimum) if we specify the browser, version, platform values.  
  

## Contributing

1. Fork it ( https://github.com/anhpham2710/iTMS-Selenium-Grid/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
