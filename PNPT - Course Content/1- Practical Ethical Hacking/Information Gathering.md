Physical - 
* breaking readers, infiltrate into company, bypass in the fencing areas
* Understanding of the company build, architectures, access logins, employee mentality.
* satelite images, drone recon, tailgating
Social - through OSINT [[OSINT Basics]]
*  search thru internet, pictures of employees,
* phone number, email id.

We/Host Assessment:
* Target Validation - whois, nslookup, dnsrecon 
	* whether the target is actual part, are we looking for? have to be strict with in the scope, as well as needs to validate completely.
* Finding Subdomains
* Fingerprinting - have to analyse how the backend and forntend app was built, hosted servers, code language and everything.

##### #Tools :
###### Discovering Email Address:

	`hunter.io`  
	`phonebook.cz`	
	`clearbit` - chrome extension will fetches the email.
	`emailhippo` - verify the email address is valid or not.

###### Hunting Breached Passwords:

	`dehashed.com`
	`hashes.org`

###### Hunting Subdomains:
	Subdomains might have the sensive data.
*.example.com 

`sublist3r -d example.com`
`crt.sh` - certificate fingerprinting information site.
`httpprobe` - checking the website alive or not.

###### Identifying website technologies:
`wappalyzer` - CMS - content management system
`https://builtwith.com`

###### Google Dorking: #dorking 
` site:*.example.com -www -ir -shop +secrets filetype:pdf `
