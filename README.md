## Multisite REST API ##  
Contributors: brettkrueger  
Tags: json, api, multisite  
Requires at least: 5.1  
Requires PHP: 7.0  
Tested up to: 6.5.5  
Stable tag: v1.3.0  
License: GPLv2 or later  
License URI: http://www.gnu.org/licenses/gpl-2.0.html  

## Description ##  

This plugin provides several endpoints for creating, listing, updating, and deleting WordPress multisites. It aims to make headless WordPress multisite environments not only possible, but practical.  

## Installation ##  

You can install this using all the usual methods. The only difference is that this plugin **must be network activated**.  

### Using The WordPress Dashboard ###  

1. Navigate to 'Add New' in the plugins dashboard
2. Search for 'multisite rest api'
3. Click 'Install Now'
4. Network Activate the plugin in the Plugin dashboard

### Uploading in WordPress Dashboard ###

1. Navigate to 'Add New' in the plugins dashboard
2. Navigate to the 'Upload' area
3. Select `multisite-rest-api.zip` from your computer
4. Click 'Install Now'
5. Network Activate the plugin in the Plugin dashboard

### Using FTP ###

1. Download `multisite-rest-api.zip`
2. Extract the `multisite-rest-api` directory to your computer
3. Upload the `multisite-rest-api` directory to the `/wp-content/plugins/` directory
4. Network Activate the plugin in the Plugin dashboard

## Upgrade Notice ##

Upgrades are pushed through WordPress.org.

## Screenshots ##

1. [Screenshot](https://raw.githubusercontent.com/brettkrueger/multisite-rest-api/main/screenshot.png)

## Changelog ##

### 1.3.0 ####
* Get or create a new user when creating a site

### 1.2.1 ####
* Fix versioning in SVN 

### 1.2.0 ###
* General quality of life improvements

### 1.1.0 ###
* Adding assign function and GET specification for /sites endpoint.

### 1.0.0 ###
* Create, List, Update, Delete multisites.

## Authentication ##

All endpoints require authentication from an existing WordPress user.
We suggest using JWT through something like [simple-jwt-login](https://wordpress.org/plugins/simple-jwt-login/).


### List Site(s) ###
- **Endpoint:** /wp-json/wp/v2/sites
- **Method:** GET
- **Args:** ["blog_id"]
- **Examples:**  
`curl -X GET /wp-json/wp/v2/sites -H "Authorization: JWT_TOKEN"`  
`curl -X GET /wp-json/wp/v2/sites/13 -H "Authorization: JWT_TOKEN"`  

### Create Site ###
- **Endpoint:** /wp-json/wp/v2/sites/create
- **Method:** POST
- **Args:** ["domain", "path", "title", "email", "password" (password will be random if empty and notify to user via email), [$options](https://developer.wordpress.org/reference/functions/wpmu_create_blog/)]
- **Examples:**  
`curl -X POST /wp-json/wp/v2/sites/create\?domain\=DOMAIN\&path\=PATH\&title\=TITLE\&email\=EMAIL\&password\=PASSWORD -H "Authorization: JWT_TOKEN"`

### Update Site ###
- **Endpoint:** /wp-json/wp/v2/sites/update
- **Method:** PUT
- **Examples:**  
`curl -X PUT /wp-json/wp/v2/sites/update\?blog_id=13&\domain\=testing13.domain.local\&admin_email\=testing13@domain.local\&title\=TESTING_13 -H "Authorization: JWT_TOKEN"`

### Delete Site ###
- **Endpoint:** /wp-json/wp/v2/sites/delete/{blog_id}
- **Method:** DELETE
- **Args:** ["blog_id"]
- **Examples:**  
`curl -X DELETE /wp-json/wp/v2/sites/delete\?blog_id\=13 -H "Authorization: JWT_TOKEN"`  
`curl -X DELETE /wp-json/wp/v2/sites/delete/13 -H "Authorization: JWT_TOKEN"`  

### Assign User to Site ###  
- **Endpoint:** /wp-json/wp/v2/sites/assign
- **Method:** PATCH  
- **ARGS:** ["user_id", "blog_id"] (defaults to current user_id)  
- **Examples:**  
`curl -X PATCH /wp-json/wp/v2/sites/assign\?blog_id\=13 -H "Authorization: JWT_TOKEN"`  
`curl -X PATCH /wp-json/wp/v2/sites/assign\?user_id=3&\?blog_id\=13 -H "Authorization: JWT_TOKEN"`  

