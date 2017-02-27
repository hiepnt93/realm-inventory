# Inventory
## A Realm Mobile Platform Example Application

<center> <img src="/Graphics/Inventory-Product-Listing.png" width="310" height="552" /></center><br>
<center> <img src="/Graphics/Inventory-Products-SortMenu.png" width="310" height="552" /></center><br>
<center> <img src="/Graphics/Inventory-Settings.png" width="310" height="552" /></center><br>



<center> <img src="/Graphics/Inventory-TakePhoto.png" width="310" height="552" /></center><br>

## Intro

This is an app designed to showcase a larger-scale collaborative example using the Realm Mobile Platform (RMP) and the Realm Object Server (ROS).

### Overview
This app is a simple implementation of an inventory tracking system designed to show 2 different ways that

# Installation

## Prerequisites

This app uses [Cocoapods](https://www.cocoapods.org) to set up the project's 3rd party dependencies. Installation can be directly (from instructions at the Cocapods site) or alternatively through a package management system like [Homebrew](brew.sh/).

### Realm Mobile Platform

This application demonstrates features of the [Realm Mobile Platform](http://lrealm.io) and needs to have a working instance of the Realm Object Server available to make tasks, and other data avalable between instances of the Fieldwork app. The Realm Mobile Platform can be downloaded from [Realm Mobile Platform](http://realm.io) and exists in two forms, a ready-to-run macOS version of the server, and a Linux version that runs on RHEL/CentOS versions 6/7 and Ununtu as well as several Amazon AMIs and Digital Ocean Droplets. The macOS version can be run with the Fieldwork right out of the box; the Linux version will require access to a Linux server.


### 3rd Party Modules

The following modules will be installed as part of the Cocoapods setup:


- [BarcodeScanner](https://github.com/hyperoslo/BarcodeScanner) an elegant barcode scanner module for iOS

- [Eureka](https://github.com/xmartlabs/Eureka) a formbuilder for iOS in Swift by xmartlabs

- [ImagePicker](https://github.com/hyperoslo/ImagePicker.git) for selection of photo library images by Hyper.no

- [PermissionScope](https://github.com/nickoneill/PermissionScope.git) permission management dialog by Nick O'Neill

## Preparing the Realm Object Server

The Inventory application can be used with any version of the Realm Object Server (Developer, Professional or Enterprise).  The Inventory app needs to be able to set permissions on the Realm used by the app - this must be done by a Realm user that has permission/rights to administer the server.  This could be the first account you set up as part of the Realm Object Server installation, or any account that has the admin bit set.

You can determine which accounts have admin rights by logging in to the Realm Object Server Dashboard:
![ROS Dashboard User Listing](/Graphics/ROS-Users-List.png)

You create new users (and give them admin rights) on this screen.

You can set the admin rights for existing users by clicking-through to the user's profile page and checking the "can administer this server" checkbox:
![ROS Dashboard User Listing](/Graphics/ROS-User-Detail.png)


Once you have created or selected an admin user to use, you can proceed with compiling and running Fieldwork.



## Compiling & Running the Application

Before attempting to compile the project, install all of its dependencies using Cocoapods by invoking ``pod install``. This is done by opening a Terminal window and changing to the directory where you downloaded the Fieldwork repository. In this main directory is a Folder called `IventoryApp` that contains `Podfile` needed by `CocoaPods` as well as the application sources.


This process will create a ``Pods`` directory which contains all of the compiled resources needed by the app, along with an Xcode xcworkspace file which you will open and work with instead
of the `Inventory.xcproject` file when building/running this application.

Once the cocoapods have been retrieved, open the ``Inventory.xcworkspace`` file and press build.  The app should compile cleanly.

### First Login

As mentioned above, the first login to the Invdntory app needs to be by a user enabled with administrative privileges on the Realm Object Server.  This is to enable a global Read/Write permission on the shared Realm that is created by the application.

### Adding Users

Adding users can be done either via the Realm Dashboard, or by adding users using the Inventory the app itself from the login screen.
<center> <img src="/Graphics/Inventory-Signup.png" width="310" height="552" /></center><br>



## Navigating Inventory
The Inventory app is a simple "tab bar" application - that is to say it supports a number of main views that are accessible at all times:

<center> <img src="/Graphics/Inventory-TabBar.png" width="621" height="71.5"/><br/>Tab Bar</center> <br/>
In this case, Inventory is very simmple and supports justr the main products list (in essence the "inventory" managed by the app) and a settings screen on which uyou can manmage your profile or log out of the app.

The app does suport several other detail screens that are explained along with the main applications screens these are:
 * Product view
 * Settings view
 * Barcode scanning view for finding existing or creating new products)
 * Product Detrail view for seeing the details of existing products
 * Product entry view for enterpring the details of a newly created product

### App Permissions
TBD
<!-- <center> <img src="/Graphics/Fieldwork-permissions.png" width="310" height="552" /><br/>Permissions</center><br>  -->

### The Products View

<center> <img src="/Graphics/Inventory-Product-Listing.png" width="310" height="552" /><br/>Product Listing</center><br>


# The Barcode Scanner & Product Detail Entry

The task list shows the tasks assigned to a given field worker, or, if the user has the "manager" role, then all tasks will be displayed.  Tapping on a tasks will reveal the task detail screen.  Managers (as shown here) have the ability to edit tasks by tapping the "Edit" button.

<center> <img src="/Graphics/Inventory-Camera-Permissions.png" width="310" height="552" /></center>Camera Permission Request<br>
<center> <img src="/Graphics/Inventory-Barcode-Simulator-Warning.png" width="310" height="552" /></center>Simulator Warning<br>
<center> <img src="/Graphics/Inventory-Barcode-Scanning.png" width="310" height="552" /></center>Barcode Scanning<br>
<center> <img src="/Graphics/Inventory-NewProduct-Scanned.png" width="310" height="552" /></center>Successful Scan<br>

# New Product Creation
A new product can be entered into Inventory in 2 ways:

  - tapping the "+" button on the product listing screen. This will bring up an empty form that can be filled in
  - Scanning a barcode - if the (UPC) scan code is not currently represented in the products
  <center> <img src="/Graphics/Inventory-Scancode-Not-Found.png" width="310" height="552" /></center>Scancode Not Found<br>

<center> <img src="/Graphics/Inventory-New-Product.png" width="310" height="552" /></center><br>


# Application Architecture

## Product Model

  - Product - This model is a minimal view of a product - it has:
      - an ID - which in our case we are using the UPC barcode number - it could be anything but using the UPC jives nicely with the bar code scanning capability
      - A product name
      - A product description
      - A product image
      -creation and modificaito dates

### Transaction Model

  - Transactions are very simple using the product ID and indicates amounts added to (positive numbers) or removed (negative numbers) from our inventory as well as the ID of which user performed the transaction.

## Person Model

  - Person - this is a simple model that maintains an avatar image, and name info for all users.  It's primary use is to allow us to have a more rich display of who performed what transactions on our products which will be added to future branches of this demo application.


### Tracking Additions and Subtractions From Inventory

One of thei8 interesting aspects of a mobil application is the fact it -- to be truly useful -- needs to work both online _and_ offline.  Ouyr inventory application as an additional constraint - it needs to suport changing quantities inside the applicaiton in a consistent and mathematically correct way.

While this may seem self-evident, supporting artithmetical atomicity is tricky.  Realm suports 2 different ways of ensuring that transacitons (additions or subtractions) from inventories: Lists and Counters.

#### Method 1: Lists

TBD: show how adding up the  numbers from a list will yield a consitent result w/out atomic counters

Let's look at a transaction log for a few hypothetical products:
<center> <img src="/Graphics/Inventory-Transaction-log-plain.png" /></center><br>

Here we see there several products - (product ID's 1,2 3 and 5) each with several additions or removals (sales)  from the inventory.

If we highlght just the acivity for product 1, we can see quickly where this goes - adding up the amounts of all the transactions tells use the current quanrtity on-hand of product #1.  This is a very safe way to implement a tranction safe coiunting system.  It also has the ability to allow us to creatre a rich system where we can add more color (metadata) to our inventory system (like the ID of who sold what, what store or region did gets credit for a sale, etc).
<center> <img src="/Graphics/Inventory-Transaction-log-highlighted.png"/></center><br>

Of course this does frequire a lot more storage and a more interaction with the server. Another way to implement the same functionality is with transaction safe counters

#### Method 2: Counters
TBS: Describe Realm Counters here...

### Conclusion
TBD: describe how using counters _and_ lisrts enable a traditional double-entry accounting system that can be used for more than just simple inventory tracking...
